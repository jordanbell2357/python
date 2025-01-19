# io.BytesIO

```
from urllib.request import urlopen
import gzip
import io

gzip_url = 'https://datasets.imdbws.com/name.basics.tsv.gz'

with urlopen(gzip_url) as response:
    gzip_bytes = response.read()

print(gzip_bytes[0:10])  # Print the first 10 bytes of the compressed data

with gzip.GzipFile(fileobj=io.BytesIO(gzip_bytes)) as gz:
    tsv_content = gz.read().decode('utf-8')

with open('name.basics.tsv', 'w') as f:
    f.write(tsv_content)
```
