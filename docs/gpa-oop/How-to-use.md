# Example input
Example input (19120338.csv), ignore file (ignore.txt), specific file (specific.txt) could be found [here](https://gist.github.com/trhgquan/ce6e4d3d97f906f71c6d51482f7de9a8)

# Input format
The input `.csv` file should look like this:

|course code|course credit|course grade|course type|
|:---------:|:-----------:|:----------:|:---------:|
|CSC10001|4|10|BB
|CSC10002|4|8.5|TC
|...|...|...|...

Course type can be any string grouped to in credit stats.

Notice that **the order of courses is essential!** If you have an input file like this:
  
|course code|course credit|course grade|course type|
|:---------:|:-----------:|:----------:|:---------:|
|CSC10001|4|10|BB
|CSC10001|4|8.5|BB

The program will give this result:
  
|course code|credits|grade (10 - scale)|grade (4 - scale)|grade (A - scale)|course type|
|:---------:|:-----:|:----------------:|:---------------:|:---------------:|:---------:|
|CSC10001|4|8.5|3.5|A|BB

This is because you've already *retaken* the `CSC10001` course, and receive
8.5 instead of 10.

## Where can I get my grade.csv?
You can use this tool [Create grade.csv file](https://github.com/khongsomeo/create-grade-csv). Notice that this requires Python >= 3.7 to run.

# Command-line arguments
Given that the program has been compiled successfully to `<PROGRAM>.exe`:

## Calculate overall GPA
```shell
./<PROGRAM> --input <GRADE_FILE.csv> --gpa
```

or, **without the `--gpa` give the same result**.
```shell
./<PROGRAM> --input <GRADE_FILE.csv> --gpa
```

## Calculate GPA of courses starts with a prefix
```shell
./<PROGRAM> --input <GRADE_FILE.csv> --specific <SPECIFIC_COURSES.txt>
```

`<SPECIFIC_COURSES.txt>` content should look like this:
```
course1prefix
course2prefix
course3prefix
```
Notice that if you use complete course code, then only one course is added,
using a prefix would choose every course to have `courseprefix` as a prefix.

## Calculate GPA but ignore some courses 
Define ignored courses inside  `<IGNORED_COURSES.txt>`, then use:
```shell
./<PROGRAM> --input <GRADE_FILE.csv> --ignore <IGNORED_COURSES.txt>
```

`IGNORED_COURSES.txt` content should look like this:
```
course1code
course2code
course3code
```

Notice that this command uses course code, **not the course's prefix**. To ignore courses with the same prefix, using `--specific` without a prefix.

## Export to `.csv` file format
```shell
./<PROGRAM> --input <GRADE_FILE.csv>
[--specific <SPECIFIC_COURSES.txt> /
    --ignore <IGNORED_COURSES.txt>] --csv
```

## Ignore parsing errors
With .csv files created by Microsoft Excel, sometimes there will be blank lines marked by commas between data blocks:
```
CSC10001,4,10,BB
,,,
CSC10002,4,8.5,BB
```

And eventually this will cause an error message logging to the screen. To ignore this: simply adding `--ignore-parsing-error` option:
```shell
./<PROGRAM> --input <GRADE_FILE.csv> [--specific <SPECIFIC_COURSES.txt> / --ignore <IGNORED_COURSES.txt>] [ --csv ] --ignore-parsing-error
```

## Ignore textart
Sometimes you just want to ignore the textart. Adding `--no-textart` will solve the problem.
```shell
./<PROGRAM> --input <GRADE_FILE.csv>
[--specific <SPECIFIC_COURSES.txt> /
--ignore <IGNORED_COURSES.txt>] [ --csv ] [ --ignore-parsing-error ]
--no-textart
```

## Custom textart
`data/textart.txt` stores the textart. Modify it with your own textart.

# Attention!
1. Default grade scale is 10.
2. 4-scale and A-scale are based on [VNUHCM -
  University of Science Student Guide 2020-21](https://www.hcmus.edu.vn/component/content/article/124-cong-tac-sinh-vien/thong-tin-danh-cho-tan-sinh-vien/3323-so-tay-sinh-vien-nam-hoc-2020-2021?Itemid=437)