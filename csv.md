# csv

```
cut -f 2 name.basics.tsv > col2.txt

tail -n +2 col2.txt | sort > col2_sorted.txt
```

```
import csv

with open('name.basics.tsv', 'r') as csv_file:
    csv_reader = csv.reader(csv_file, delimiter='\t')

    for k, row in enumerate(csv_reader):
        if k < 10:
            print(row[1])
        else:
            break

    name_list = [row[1] for row in csv_reader]
    
    name_list_newline = [name + '\n' for name in name_list[0:-1]] + [name_list[-1]]

    with open('names.txt', 'w') as output_file:
        output_file.writelines(name_list_newline)
```
