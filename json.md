# json

```python
# csv_to_json.py
# head -n 5 name.basics.tsv > name.head.tsv

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
            json.dump(row, json_file, separators=(',', ':'), ensure_ascii=False, indent=2)
        for row in csv_reader:
            row = {k: (None if v == r'\N' else v) for k, v in row.items()}
            if row['birthYear'] is not None:
                row['birthYear'] = int(row['birthYear'])
            if row['deathYear'] is not None:
                row['deathYear'] = int(row['deathYear'])
            json_file.write(',\n')  # Add a comma and newline before each subsequent row
            json.dump(row, json_file, separators=(',', ':'), ensure_ascii=False, indent=2)

        json_file.write('\n]\n')  # End the JSON array
```

```bash
head -n 2 name.head.json
# [
# {"nconst":"nm0000001","primaryName":"Fred Astaire","birthYear":"1899","deathYear":"1987","primaryProfession":"actor,miscellaneous,producer","knownForTitles":"tt0072308,tt0050419,tt0053137,tt0027125"},
```

```console
tail -n 2 name.head.json
{"nconst":"nm0000004","primaryName":"John Belushi","birthYear":1949,"deathYear":1982,"primaryProfession":"actor,writer,music_department","knownForTitles":"tt0072562,tt0077975,tt0080455,tt0078723"}
]
```

```bash
jq . name.head.json
```

```json
[
  {
    "nconst": "nm0000001",
    "primaryName": "Fred Astaire",
    "birthYear": 1899,
    "deathYear": 1987,
    "primaryProfession": "actor,miscellaneous,producer",
    "knownForTitles": "tt0072308,tt0050419,tt0053137,tt0027125"
  },
  {
    "nconst": "nm0000002",
    "primaryName": "Lauren Bacall",
    "birthYear": 1924,
    "deathYear": 2014,
    "primaryProfession": "actress,soundtrack,archive_footage",
    "knownForTitles": "tt0037382,tt0075213,tt0117057,tt0038355"
  },
  {
    "nconst": "nm0000003",
    "primaryName": "Brigitte Bardot",
    "birthYear": 1934,
    "deathYear": null,
    "primaryProfession": "actress,music_department,producer",
    "knownForTitles": "tt0057345,tt0049189,tt0056404,tt0054452"
  },
  {
    "nconst": "nm0000004",
    "primaryName": "John Belushi",
    "birthYear": 1949,
    "deathYear": 1982,
    "primaryProfession": "actor,writer,music_department",
    "knownForTitles": "tt0072562,tt0077975,tt0080455,tt0078723"
  }
]
```

```bash
python3 -m json.tool name.head.json
```

```json
[
    {
        "nconst": "nm0000001",
        "primaryName": "Fred Astaire",
        "birthYear": 1899,
        "deathYear": 1987,
        "primaryProfession": "actor,miscellaneous,producer",
        "knownForTitles": "tt0072308,tt0050419,tt0053137,tt0027125"
    },
    {
        "nconst": "nm0000002",
        "primaryName": "Lauren Bacall",
        "birthYear": 1924,
        "deathYear": 2014,
        "primaryProfession": "actress,soundtrack,archive_footage",
        "knownForTitles": "tt0037382,tt0075213,tt0117057,tt0038355"
    },
    {
        "nconst": "nm0000003",
        "primaryName": "Brigitte Bardot",
        "birthYear": 1934,
        "deathYear": null,
        "primaryProfession": "actress,music_department,producer",
        "knownForTitles": "tt0057345,tt0049189,tt0056404,tt0054452"
    },
    {
        "nconst": "nm0000004",
        "primaryName": "John Belushi",
        "birthYear": 1949,
        "deathYear": 1982,
        "primaryProfession": "actor,writer,music_department",
        "knownForTitles": "tt0072562,tt0077975,tt0080455,tt0078723"
    }
]
```
