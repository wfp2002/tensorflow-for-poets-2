Fonte:
https://codelabs.developers.google.com/codelabs/tensorflow-for-poets

Instalando no linux o tensorflow direto por PIP
pip install tensorflow


Instalando via Docker
docker pull tensorflow/tensorflow                  
docker run -it -p 8888:8888 tensorflow/tensorflow  


Clonando o repositorio

git clone https://github.com/googlecodelabs/tensorflow-for-poets-2

ou 

git clone https://github.com/wfp2002/tensorflow-for-poets-2
cd tensorflow-for-poets-2

Baixando imagens de flores para treino
curl http://download.tensorflow.org/example_images/flower_photos.tgz | tar xz -C tf_files

Checando imagens
ls tf_files/flower_photos

Retreinar as imagens

Setar as variaveis de ambiente
IMAGE_SIZE=224
ARCHITECTURE="mobilenet_0.50_${IMAGE_SIZE}"

Start tensorflow
tensorboard --logdir tf_files/training_summaries &

Rodar Treinamento (Para uma melhor acuracia alterar os steps de 500 para uns 2000 o defaul e 4000
python -m scripts.retrain \
  --bottleneck_dir=tf_files/bottlenecks \
  --how_many_training_steps=500 \
  --model_dir=tf_files/models/ \
  --summaries_dir=tf_files/training_summaries/"${ARCHITECTURE}" \
  --output_graph=tf_files/retrained_graph.pb \
  --output_labels=tf_files/retrained_labels.txt \
  --architecture="${ARCHITECTURE}" \
  --image_dir=tf_files/flower_photos


Para acessar o tensorflow web
0.0.0.0:6006


Teste para ver se detecta uma imagem
python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/flower_photos/daisy/21652746_cc379e0eea_m.jpg


python -m scripts.label_image \
    --graph=tf_files/retrained_graph.pb  \
    --image=tf_files/flower_photos/roses/2414954629_3708a1a04d.jpg 


