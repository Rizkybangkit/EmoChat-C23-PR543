# Deploying model to Cloud Function
GCP services used:
* Cloud Function
* Cloud Storage
* Pubsub
## GCP architecture
![GCP architecture](https://github.com/Rizkybangkit/EmoChat-C23-PR543/assets/91662109/733f108b-ec0b-4e7f-badf-76cd0b66a027)
## Steps
1. Make bucket
```
gsutil mb -l asia-southeast2 gs://audio-bucket-95
```
2. Make Pubsub topic
```
gcloud pubsub topics create prediction-result
``` 
3. Clone the function
```
git clone --branch cloud-computing https://github.com/Rizkybangkit/EmoChat-C23-PR543.git
```
4. Path to the function folder
```
cd function
``` 
5. Deploy to the cloud function
```
gcloud functions deploy process_uploaded_audio \
    --runtime python310 \
    --region asia-southeast2 \
    --trigger-resource audio-bucket-95 \
    --entry-point process_uploaded_audio \
    --memory 1024Mi \
    --trigger-event google.storage.object.finalize
```  

