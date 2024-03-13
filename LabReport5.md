# Lab Report 5 - Putting It All Together

Flora Kang

## Part 1 - Debugging Scenario

(base code: Skill Demo 3 Practice)

**Student**: Please help! When I run the bash script [grade.sh](http://grade.sh), the result.txt file is not created for student4, student5, and student6. The compile-errors.txt file is also created in the wrong folder - in student3.

Here is my code so far and the resulting output

(important lines labeled for reference)

`grade.h`

```bash
original_dir=`pwd` # line 1

for submission_dir in submissions/* # line 3
do
	echo $submission_dir
  cd $submission_dir # line 6

  javac Sorter.java # line 8

  # Replace this with a condition that does the appropriate check
  if [[ $? -ne 0 ]] # line 11
  then
    echo "$submission_dir: Compile error" > result.txt # line 13    
    continue # line 14
  else # line 15
    echo "Compile successful for $submission_dir"
  fi

  passed=0
  failed=0
  for test_file in $original_dir/test-data/*.txt
  do
    result=`java Sorter < $test_file`
    expect=`cat $test_file.expect`
    if [[ $expect == $result ]]
    then
      passed=$(( $passed+1 ))
    else
      failed=$(( $failed+1 ))
    fi
  done
  echo "$submission_dir: Test results: $passed passed, $failed failed" > result.txt
  cd $original_dir # line 33
done

all_results=`find submissions -name "result.txt"`
cat $all_results | grep "Compile error"  > compile-errors.txt

# Here, add code to put all of the results for files that successfully ran into
# run-results.txt

for result_file in submissions/*/result.txt; do
    if ! grep "Compile error" "$result_file"; then
        cat "$result_file" >> run-results.txt
    fi
done

```

```bash
$ bash grade.sh
submissions/student1
Compile successful for submissions/student1
submissions/student2
Compile successful for submissions/student2
submissions/student3
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
    ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
                               ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
    ^
  symbol:   class Scanner
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
                     ^
  symbol:   class Scanner
  location: class Sorter
4 errors
submissions/student4
grade.sh: line 6: cd: submissions/student4: No such file or directory
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
    ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
                               ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
    ^
  symbol:   class Scanner
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
                     ^
  symbol:   class Scanner
  location: class Sorter
4 errors
submissions/student5
grade.sh: line 6: cd: submissions/student5: No such file or directory
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
    ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
                               ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
    ^
  symbol:   class Scanner
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
                     ^
  symbol:   class Scanner
  location: class Sorter
4 errors
submissions/student6
grade.sh: line 6: cd: submissions/student6: No such file or directory
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
    ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:3: error: cannot find symbol
    ArrayList<Integer> a = new ArrayList<>();
                               ^
  symbol:   class ArrayList
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
    ^
  symbol:   class Scanner
  location: class Sorter
Sorter.java:4: error: cannot find symbol
    Scanner in = new Scanner(System.in);
                     ^
  symbol:   class Scanner
  location: class Sorter
4 errors
find: ‘submissions’: No such file or directory
```

**TA**: Try walking through your current code and take note of where your current working directory is at each step.

**Student**: Thank you! Here are my notes from taking your advice:

![IMG_8390](https://github.com/fk-kny/cse15l-lab-reports/assets/158122319/89e683f3-740d-43fb-8a21-92ee807950c8)


I realize now that in the iterations when Sorter.java fails to compile, the if statement evaluates as true and within this block, I have `continue` which tells the program to exit the current iteration and skip to the next. This was an issue because we have our code changing the working directory back to the original directory later on within the for loop. Consequently, the working directory stays at the `submission_dir` it was assigned at the beginning of the loop and at the next iteration, line 6 searches for the next submissions/* but fails to find the proper next directory.

This bug can be easily fixed by adding a line of code within the if block to reassign the working directory to the original directory, which we conveniently have saved as `original_dir`

Here is the line to insert: `cd $original_dir` in between lines 13 and 14.
After fixing this, my code ran correctly.

## Part 2 - Reflection

In the second half of the quarter, I learned about bash and working from the command line. Before this class, I was not aware what bash was, how it worked, or how to write it. I enjoyed learning how to write bash scripts and was happily surprised to see the logic was similar to that of Java, which I am much more familiar with. I enjoyed learning vim. While this took me quuite a while to learn how to navigate, Once I got the hang of it, I enjoyed seeing just how efficiently I could perform actions such as editing code, making files, etc.
