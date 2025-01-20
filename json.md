# json

```python
# csv_to_json.py
# head -n 20 name.basics.tsv > name.head.tsv

import csv
import json

TSV_FILE_PATH = 'name.head.tsv'
JSON_FILE_PATH = 'name.head.json'

with open(TSV_FILE_PATH, 'r', encoding='utf-8') as tsv_file:
    csv_reader = csv.DictReader(tsv_file, delimiter='\t')
    with open(JSON_FILE_PATH, 'w', encoding='utf-8') as json_file:
        json_file.write('[\n')  # Start the JSON array
        row = next(csv_reader)
        row = {k: (None if v == r'\N' else v) for k, v in row.items()}
        if row['birthYear'] is not None:
            row['birthYear'] = int(row['birthYear'])
        if row['deathYear'] is not None:
            row['deathYear'] = int(row['deathYear'])
            json.dump(row, json_file, separators=(',', ':'), ensure_ascii=False)
        for row in csv_reader:
            row = {k: (None if v == r'\N' else v) for k, v in row.items()}
            if row['birthYear'] is not None:
                row['birthYear'] = int(row['birthYear'])
            if row['deathYear'] is not None:
                row['deathYear'] = int(row['deathYear'])
            json_file.write(',\n')  # Add a comma and newline before each subsequent row
            json.dump(row, json_file, separators=(',', ':'), ensure_ascii=False)

        json_file.write('\n]\n')  # End the JSON array
```

```bash
head -n 2 name.head.json
# [
# {"nconst":"nm0000001","primaryName":"Fred Astaire","birthYear":"1899","deathYear":"1987","primaryProfession":"actor,miscellaneous,producer","knownForTitles":"tt0072308,tt0050419,tt0053137,tt0027125"},
```

```bash
tail -n 2 name.head.json
# {"nconst":"nm0000019","primaryName":"Federico Fellini","birthYear":1920,"deathYear":1993,"primaryProfession":"writer,director,actor","knownForTitles":"tt0056801,tt0053779,tt0047528,tt0071129"}
# ]
```

```bash
jq '.[0]' name.head.json
{
  "nconst": "nm0000001",
  "primaryName": "Fred Astaire",
  "birthYear": 1899,
  "deathYear": 1987,
  "primaryProfession": "actor,miscellaneous,producer",
  "knownForTitles": "tt0072308,tt0050419,tt0053137,tt0027125"
}
```
