# zipfile

```python
from zipfile import ZipFile
import io
from urllib.request import urlopen

zip_url = "https://storage.googleapis.com/tensorflow/tf-keras-datasets/jena_climate_2009_2016.csv.zip"

with urlopen(zip_url) as response:
    zip_bytes = response.read()

with ZipFile(io.BytesIO(zip_bytes)) as z:
    csv_contents = z.read("jena_climate_2009_2016.csv").decode(encoding="utf-8")

df = pd.read_csv(io.StringIO(csv_contents))
```
