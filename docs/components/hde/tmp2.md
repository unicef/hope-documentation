 

Create Deduplication Set: deduplication_set (POST) 

 
 

deduplication_set/<id>/images (POST) 

deduplication_set/<id>/image_bulk (POST) 

 
 

deduplication_set/<id>/process (POST) 

 

------ 

 

 

Deduplication Engine App 

 

Celery 

 

Neural Network Model (DNN) 

 

 

Blob Stob Storages 

 

1) HOPEAzureStorage: Read only storage for hope pictures 

 

2) HDEAzureStorage 

static-dde: 

enconding-dde: Storage for encoding? Numpy vectors 

models-dde:  

Coffee model 

Prototext file 

 

 

Service use 3 azure containers: 

AZURE_CONTAINER_HDE  - writable container for encodings data 

AZURE_CONTAINER_HOPE - read-only container for images from HOPE 

AZURE_CONTAINER_DNN - read-only container for DNN files (deploy.prototxt and res10_300x300_ssd_iter_140000.caffemodel) 

Depending on constance.config.DNN_FILES_SOURCE, the service fetches DNN files from GitHub or AZURE_CONTAINER_DNN using celery task. 

At startup, the absence of local DNN files triggers an automatic download. 

For manual interventions, access the admin panel at: Home › Faces › DNN files. 

We drop downloaded files into the settings.CV2DNN_DIR folder.CV2DNN_DIR. This folder must be reached by our backend and Celery workers. 

At the future the files within the AZURE_CONTAINER_DNN can be automatically updated with new versions of our trained model via a dedicated pipeline. 