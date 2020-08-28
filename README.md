# Cohen Kappa Calculator
![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)

Python-based calculator of the inter-rater reliability measure Cohen's Kappa using Excel as a database of the raw instance values. 

## Explanation

```python
file = askopenfile(mode="r", filetypes = [("Excel Files", "*.xlsx")])
wb = load_workbook(file.name)
ws = wb["Sheet1"]
rater1 = ws["A"]
rater2 = ws["B"]
r1_val = [rater1[x].value for x in range(1,len(rater1))]
r2_val = [rater2[x].value for x in range(1,len(rater2))]
    
root = Tk()
button = tk.Button(root, text="Open", command=UploadAction)
button.pack()

root.destroy()
root.mainloop()
```

Using tkinter to prompt an Excel upload file.
* Note that the code begins from the second cell of each column, assuming the first cell is a place     marker for Rater 1/ Rater 2 titles.

Given that the data is inputted in columns A and B, the data is then placed into two lists. The tkinter window can then be freely closed.

```python
r1_n_val = []
r2_n_val = []

if len(r1_val) == sum(r1_val)+1:
    for x in r1_val:
        if x>0:
            r1_n_val.append(1)
        else: 
            r1_n_val.append(0)

    for x in r2_val:
        if x>0:
            r2_n_val.append(1)
        else: 
            r2_n_val.append(0)
    kappa_score = cohen_kappa_score(r1_n_val, r2_n_val)
    if math.isnan(kappa_score) == True:
        print(1.0)
    else:
        print(kappa_score)
else:
    kappa_score = cohen_kappa_score(r1_val, r2_val)
    if math.isnan(kappa_score) == True:
        print(1.0)
    else:
        print("The Cohen Kappa score is: "+str(kappa_score))
```

If the original data can be directly compared, the code continues directly to the initial else portion, printing the Cohen Kappa score. 

As the original project examined various counts of data which needed to be evaluated as either 0 or a non-zero, the major portion evaluates 0's as 0's and non-zero's as 1's and inputs them into new lists, which is then utilized to calculate the Cohen Kappa score. 

```python
table = f"""
Poor           = < 0.00
Slight         = 0.00 - 0.20
Fair           = 0.20 - 0.40
Moderate       = 0.41 - 0.60
Substanstial   = 0.61 - 0.80
Almost Perfect = 0.81 - 1.00
"""
print(table)
```

Prints a descriptive table of how to evaluate the generated Cohen Kappa score. 
