# Cloud-based Distributed Search Engine

**NOTICE:** Due to the academic policy, the source code is excluded.

## Run
Make sure you are in the `backend` directory.

### 0. Install Java

### 1. Compile
```bash
bash script/build.sh
```

### 2. Start master and workers
```bash
bash script/start_workers.sh <flame_master_port> <kvs_master_port> <flame_worker_num> <kvs_worker_num> <ip>
```
Defalt value:
```
flame_master_port: 9000
kvs_master_port: 8000
flame_worker_num: 3
kvs_worker_num: 4
ip: your public IP
```
Note:
+ You can use remote IP and port in `flame_master_port` and `kvs_master_port`, such as `1.1.1.1:8000`. This will help if you want to deploy the masters and the workers in different servers.
+ If you use remote IP and port in the above two fields, the script will not start the corresponding masters. If you use only port, the master will be started locally.
+ If your worker is not accessible on the above `ip`, the script will fail to start your masters and workers.

An example command of using this script for local test is:
```bash
bash script/start_workers.sh 9000 8000 2 8 127.0.0.1
```
An example command of using this script for distributed deployments is:
```bash
# Masters
bash script/start_workers.sh 9000 8000 0 0

# Workers
bash script/start_workers.sh 1.2.3.4:9000 1.2.3.48000 1 1
```

### 3. Start jobs
To start `Crawler`, run
```bash
bash script/crawl.sh
```
The crawled data will be saved in `crawl.table`.

To start `IndexerTFIDF`, run
```bash
bash script/indexer.sh
```
The TF table the IDF table will be saved in `tf-table.table` and `idf-table.table` respectively.

To start `PageRank`, run
```bash
bash script/pagerank.sh <threshold>
```
`threshold` is a decimal fraction, such as 0.01. The PageRank table will be saved in `pageranks.table`.

### Start Frontend and Backend
```bash
java -Dfile.encoding=UTF-8 -cp out/production/backend:lib/* cis5550.backend.Server
```

## Third-party libraries
+ [jsoup](https://jsoup.org/)
+ [gson](https://github.com/google/gson)
+ [axios](https://www.npmjs.com/package/axios)
```
axios is imported to our frontend by
<script src="https://cdn.jsdelivr.net/npm/axios@1.1.2/dist/axios.min.js"></script>
```
+ [bootstrap](https://getbootstrap.com/)
```
bootstrap is imported to our frontend by
<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-KK94CHFLLe+nY2dmCWGMq91rCGa5gtU4mk92HdvYe+M/SXH301p5ILy+dN9+nJOZ" crossorigin="anonymous">
```
+ [Bing spellcheck API](https://www.microsoft.com/en-us/bing/apis/bing-web-search-api)

