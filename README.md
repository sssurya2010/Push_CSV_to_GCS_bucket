# Push_CSV_to_GCS_bucket
Here is a simple python code with google cloud packages that can help you push your csv files to a GCS bucket. Later you can use these csv's in the GCS bucket as a raw layer of data processing them to Bigquery for analysis.

# Packages Needed
    from google.cloud import storage as gcs
    from datetime import datetime as dt

# Define a function to push the file
    def push_to_gcs(bucket_name, source_file_name, destination_blob_name):
    """
    Uploads a file to Google Cloud Storage.

    Args:
        bucket_name (str): The name of the GCS bucket.
        source_file_name (str): The local path to the file to upload.
        destination_blob_name (str): The name of the blob in GCS.

    Returns:
        str: The public URL of the uploaded file.
    """
    storage_client = gcs.Client()
    bucket = storage_client.bucket(bucket_name)
    blob = bucket.blob(destination_blob_name)

    blob.upload_from_filename(source_file_name)

# Call the function with parameters

    push_to_gcs(
    bucket_name='your-bucket-name',
    source_file_name='path/to/your/local/file.txt', 
    destination_blob_name=f'uploads/{dt.now().strftime("%Y%m%d_%H%M%S")}_file.txt'
    )
