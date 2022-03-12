# Google Cloud Firebase

## List bucket
gsutil ls gs://mediateprototype.appspot.com/logged-frames/read/ 

## Download single file from bucket
gsutil cp gs://mediateprototype.appspot.com/share/1563207233036_cH64I1-_3_Y_s5.jpg ./download_dir


## Download multiple files
some_program | gsutil -m cp -I ./download_dir

## Download whole bucket
gsutil -m cp -R gs://<bucket_name> $local_folder

## Upload single file
gsutil cp rotated-read.tar gs://mediateprototype.appspot.com/share/

## Upload multiple files
gsutil -m cp *.jpg gs://<bucket_name>
some_program | gsutil -m cp -I gs://<bucket_name>

## Upload directory tree
gsutil -m cp -r $local_folder gs://<bucket_name>


## useful

cat labelled-images.txt | tr '\n' '\0' | xargs -0 -n 1 -I{} echo 'gs://mediateprototype.appspot.com/logged-frames/read/{}' | gsutil -m cp -I ./labelled-images/


## Database read write permission per user

{
  "rules": {
    "iosUserAppData": {
      "$uid": {
        ".read": "$uid === auth.uid",
        ".write": "$uid === auth.uid"
      }
    }
  }
}
