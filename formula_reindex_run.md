Indexing complete.
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % source venv/bin/activate && python3 search.py --query "how do databases work?"
Loading FAISS index from 'faiss_index.bin'...
Loading file paths from 'filepaths.txt'...
Loading sentence transformer model...
Searching for: 'how do databases work?'

Top 5 search results:
1. ./docs/databases.md (Distance: 0.4158)
2. ./docs/data_structures.md (Distance: 1.1145)
3. ./docs/machine_learning.md (Distance: 1.4331)
4. ./docs/sample.md (Distance: 1.4334)
5. ./docs/cybersecurity.md (Distance: 1.4671)
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % ls -an
total 1928
drwxr-xr-x  19 501  20     608 Oct  8 07:22 .
drwxr-xr-x  58 501  20    1856 Oct  8 06:54 ..
drwxr-xr-x  14 501  20     448 Oct  8 07:22 .git
-rw-r--r--   1 501  20      49 Oct  8 07:11 .gitignore
-rw-r--r--   1 501  20     222 Oct  8 06:54 README.md
-rw-r--r--   1 501  20    1823 Oct  8 07:13 USAGE.md
-rw-r--r--   1 501  20    3673 Oct  8 07:14 architecture.md
-rw-r--r--   1 501  20    1606 Oct  8 07:02 cline.md
drwxr-xr-x  13 501  20     416 Oct  8 07:17 docs
-rw-r--r--   1 501  20   17074 Oct  8 07:21 faiss_index.bin
-rw-r--r--   1 501  20     254 Oct  8 07:21 filepaths.txt
-rw-r--r--   1 501  20    2093 Oct  8 07:15 goals.md
-rw-r--r--   1 501  20    2442 Oct  8 07:02 index.py
-rw-r--r--   1 501  20      53 Oct  8 07:02 requirements.txt
-rw-r--r--   1 501  20    1815 Oct  8 07:02 search.py
-rw-r--r--   1 501  20     334 Oct  8 07:10 todo.md
-rw-r--r--   1 501  20     929 Oct  8 07:22 ui_user_experience.md
-rw-r--r--   1 501  20  914344 Oct  8 07:22 vector_database.png
drwxr-xr-x   8 501  20     256 Oct  8 07:11 venv
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % source venv/bin/activate && python3 search.py --query "how do databases work?"
Loading FAISS index from 'faiss_index.bin'...
Loading file paths from 'filepaths.txt'...
Loading sentence transformer model...
Searching for: 'how do databases work?'

Top 5 search results:
1. ./docs/databases.md (Distance: 0.4158)
2. ./docs/data_structures.md (Distance: 1.1145)
3. ./docs/machine_learning.md (Distance: 1.4331)
4. ./docs/sample.md (Distance: 1.4334)
5. ./docs/cybersecurity.md (Distance: 1.4671)
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % python3 search.py --query "who is mehmet"                                     
Loading FAISS index from 'faiss_index.bin'...
Loading file paths from 'filepaths.txt'...
Loading sentence transformer model...
Searching for: 'who is mehmet'

Top 5 search results:
1. ./docs/databases.md (Distance: 1.8730)
2. ./docs/version_control.md (Distance: 1.9212)
3. ./docs/devops.md (Distance: 1.9443)
4. ./docs/cybersecurity.md (Distance: 1.9989)
5. ./docs/cloud_computing.md (Distance: 2.0312)
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % python3 index.py                         
usage: index.py [-h] --folder FOLDER
index.py: error: the following arguments are required: --folder
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % source venv/bin/activate && python3 index.py --folder ./docs                  
Loading sentence transformer model...
Scanning for markdown files in './docs'...
Found 12 markdown files. Creating embeddings...
Saving FAISS index to 'faiss_index.bin'...
Saving file paths to 'filepaths.txt'...
Indexing complete.
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % python3 search.py --query "who is mehmet"                   
Loading FAISS index from 'faiss_index.bin'...
Loading file paths from 'filepaths.txt'...
Loading sentence transformer model...
Searching for: 'who is mehmet'

Top 5 search results:
1. ./docs/mehmet.md (Distance: 1.2084)
2. ./docs/databases.md (Distance: 1.8730)
3. ./docs/version_control.md (Distance: 1.9212)
4. ./docs/devops.md (Distance: 1.9443)
5. ./docs/cybersecurity.md (Distance: 1.9989)
(venv) rifaterdemsahin@Rifats-MacBook-Pro rag % 