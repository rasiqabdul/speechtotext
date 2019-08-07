# speechtotext
Speech to text using aws transcribe

Prerequisites
1)	Install Ubuntu on Windows 10
-	Go to Microsoft market place on your windows 10 computer.
-	Search for linux on windows and install ubuntu app.
 
2)	Launch Ubuntu app from start menu and install below packages.
-	Install ffmpeg for converting flv files to mp3 files.
$sudo apt-get install ffmpeg
-	Install jq for parsing json data 
$sudo apt-get install jq
-	Install aws cli using pip
$pip3 install awscli --upgrade –user
3)	AWS account and IAM user with admin privileges required(Full access to all resources)
-	Download secret access key and access key for IAM user from console.
-	Configure aws cli in ubuntu by running below commands.
$aws configure
AWS Access Key ID [None]: AKI*********DFRT
AWS Secret Access Key [None]: wJalr********************KEY
Default region name [None]: us-east-1
Default output format [None]: 
4)	Install any dependent OS packages if required.
 
3	Setup Environment
1)	Create local directory structure.
Directory	Description
/home/user/transcribe/flvfiles	All input flv files should be in this folder
/home/user/transcribe/mp3files	All converted mp3 files will be saved in this folder
/home/user/transcribe/jsonfiles	All json files will be saved in this folder
/home/user/transcribe/textfiles	Result with converted text files will be saved in this folder
/home/user/transcribe/src	Source code or script to convert speech to text will be in this folder.

2)	Create S3 Buckets from AWS console.
S3 Bucket	Description
s3://transcribeinput	Input bucket for transcribe 
s3://transcribeoutput	Output bucket for transcribe

4	Run Transcribe to convert FLV files to TEXT
1)	Unzip transcribe.zip file in your home directory.
2)	Copy all flv files which needs to be converted to text into.
/home/user/transcribe/flvfiles/ Folder
3)	Running script guide.
/home/user/transcribe/src/flvtotext.sh \         Shell script to convert flv to text
'/home/user/transcribe/flvfiles' \                       First argument flv folder path
'/home/user/transcribe/mp3files/' \                  Second argument mp3 folder path 
's3://transcribeinput' \                                           Third argument input s3 bucket 
'transcribeoutput' \                                        Fourth argument output s3 bucket
'/home/user/transcribe/jsonfiles/' \                    Fifth argument json folder path
'/home/user/transcribe/textfiles/' \      Sixth argument textfiles/final result folder path
300                                                                Wait time for transcriber to convert input data

IMPORTANT NOTE : Change the wait time argument accordingly for number of files being processed. AWS transcribe takes around 120 seconds per file to transcribe.

4)	Run flvtotext.sh script from command line.
/home/user/transcribe/src/flvtotext.sh '/home/user/transcribe/flvfiles' '/home/user/transcribe/mp3files/' 's3://transcribeinput' 'transcribeoutput' '/home/user/transcribe/jsonfiles' '/home/user/transcribe/textfiles/' 300


