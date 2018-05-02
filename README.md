## Browser uploads to Minio via EvaporateJS

Sample program to benchmark file uploads to Minio server using EvaporateJS library.

#### Note

- Program will upload 1000 copies of same file to Minio server and report the elapsed time.
- EvaporateJS is edited to not compute Content-MD5 (`computeContentMd5: false`) for each request.
- Part size is set to 6 MB.

### 1. Start Minio Server

Start a Minio server instance using the steps mentioned [here](https://docs.minio.io/docs/minio-quickstart-guide). Make a note of access key, secret key and region. By default Minio region is set to `us-east-1`. Once server is up, create a bucket using client of your choice.

### 2. Start Signing Server

Install dependencies using

```sh
npm install express body-parser
```

Set the signing server environment variables

```sh
export AWS_SECRET=<MINIO_SECRET_KEY>
export AWS_REGION=<MINIO_REGION>
export AWS_SERVICE=s3
```

Then, start the signing server by

```sh
./signing_server.js
```

### 3. Configure EvaporateJS Library

Open the file `evaporate_minio.html` and update the following sections

```sh
aws_key: '<MINIO_ACCESS_KEY>',
bucket: '<MINIO_BUCKET>',
awsRegion: '<MINIO_REGION>',
aws_url: '<MINIO_ENDPOINT>',
```

You can also configure MD5 calculation and default part size using fields

```sh
computeContentMd5: false,
partSize:  6 * 1024 * 1024,
```

### 4. Upload files

Access the signing server via your browser. By default it runs on `http://localhost:3000`. Select a file to upload. EvaporateJS will start uploading 1000 instances of the same file, once the upload is complete, you'll get a browser alert with total time taken in uploading the files.
