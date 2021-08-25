# torchserve-r2gen-model

## create .mar file

clone torchserve and compress to zip format

```
git clone https://github.com/pytorch/serve.git
```

```
torch-model-archiver --model-name r2gen -v 1.0 --model-file model.py --serialized-file model_iu_xray.pth --export-path model-store --extra-files requirements.txt,att_model.py,encoder_decoder.py,utils.py,caption_model.py,visual_extractor.py,tokenizers.py,annotation.json,handler.py,serve.zip --handler my_handler.py -f
```
## run torchserve

docker run --rm -it -p 3000:8080 -p 3001:8081 -v "$(pwd)"/model-store:/home/model-server/model-store pytorch/torchserve:latest torchserve --start --model-store model-store --models r2gen=model-store/r2gen.ma
