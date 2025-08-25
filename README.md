# Vertical chart from array with random values at each run

Ex. (198) - Vertical chart from array with random values at each run, is presented here in three programming languages: Python, MATLAB, and JavaScript. Although the implementations differ in syntax, the underlying concept remains identical across all three versions. Each code sample is reproduced from its respective volume of the series <i>Coding Examples from Simple to Complex</i> (Springer, 2024).
***

Compared to the previous example, the new implementation brings the ASCII axis for this chart and the ability to view the chart with different values each time the code is run. Thus, the given code creates a visual representation of data in the form of a bar chart using ASCII characters. The code begins by declaring an empty array a and a variable n with a value of 9. A for-loop iterates from 0 to n-1 (0 to 8 in this case), generating random integer values between 0 and 99 using randint(), and stores them in the array a. The source code prints the result of the SMC(chart(a)) function, which generates a bar chart from the array a and then prints a visual representation of the chart. The chart(a) function is defined next. It takes an array a as its parameter. Inside the function, it initializes variables m and t, and it calculates the maximum value in the array a by using the max(a, default=1) function. We use the second parameter as default=1 to avoid division by zero. A nested for-loop is able to construct the visual representation of the bar chart, using Unicode block characters (▓ and ░) to represent the data. The result is stored in the t array, which is returned at the end. The SMC(a) function is defined to create a string representation of the bar chart. It takes an array a as its parameter, representing the bar chart. It calculates the dimensions of the chart, initializes an empty string r, and then constructs the chart using nested loops. The loops iterate through the array a and construct the chart row by row, with underscores (“_”) at the bottom, “|” to separate the data from the labels, and labels for each column at the top. The resulting string r represents the bar chart and is then returned. In the end, the code prints the chart using print(SMC(chart(a))), followed by a new line character and a display of the original data array a.

## Example in Python:

```python
import random

a = [0] * 9
n = 9

for k in range(n):
    a[k] = random.randint(0, 99)

def chart(a):
    m = 9
    t = [['' for _ in range(n)] for _ in range(m)]

    # Use default=1 to avoid 
    # division by zero.

    max_val = max(a, default=1)

    for j in range(m):
        for i in range(n):

            f = int((m / max_val) * a[i])
            t[m - j - 1][i] = '\u2591'

            if j < f:
                t[m - j - 1][i] = '\u2593'
    
    return t

def SMC(a):
    n = len(a)
    m = len(a[0])
    r = ''
    
    for i in range(n + 2):
        for j in range(m):
            if i < n:
                r += a[i][j]
            if i == n:
                r += '|'
            if i > n:
                r += str(j + 1)
        if i == n:
            r += '\n'
        if i < n:
            r += "_" + str(n - i) + "\n"
    
    return r

print(SMC(chart(a)))
print('\n' + str(a))
``` 

```text
Python output:

░░░░░░░▓░_9
░░░░░░░▓░_8
░▓░░▓░░▓░_7
░▓░░▓░░▓░_6
░▓▓░▓░▓▓░_5
░▓▓░▓░▓▓░_4
▓▓▓▓▓░▓▓▓_3
▓▓▓▓▓▓▓▓▓_2
▓▓▓▓▓▓▓▓▓_1
|||||||||
123456789

[35, 76, 50, 32, 76, 21, 54, 89, 39]
```

## Example in Javascript:

```javascript
let a = [];
let n = 9;

for(let k=0; k<n; k++){
    a[k] = Math.floor(Math.random() * 100);
}

print(SMC(chart(a)));
print('\n' + a);

function chart(a){
    let m = 9;
    let t = [];
    let max = Math.max.apply(null, a);
    
    for(let j=0; j<m; j++){
        t[m-j-1] = [];
        for(let i=0; i<n; i++)
        {
            f = Math.floor((m/max) * a[i]);
            t[m-j-1][i] = '\u2591';
            if(j < f){t[m-j-1][i] = '\u2593';}
        }
    }
    return t;
}

function SMC(a) {
    let n = a.length;
    let m = a[0].length;
    let r = '';
    
    for(let i=0; i<n+2; i++) {
        for(let j=0; j<m; j++) {
            if(i<n){r += a[i][j];}
            if(i==n){r += '|';}
            if(i>n){r += j+1;}
        }
        if(i==n){r += '\n';}
        if(i<n){r += "_" + (n-i) + "\n";}
    }
    return r;
}
```

```text
Javascript output:

░░▓░░░░░░_9
░░▓░░░░░░_8
░▓▓░░░▓░░_7
░▓▓░░░▓▓░_6
░▓▓▓▓▓▓▓░_5
▓▓▓▓▓▓▓▓░_4
▓▓▓▓▓▓▓▓▓_3
▓▓▓▓▓▓▓▓▓_2
▓▓▓▓▓▓▓▓▓_1
|||||||||
123456789

[49, 77, 96, 57, 56, 55, 82, 64, 37]
```

## Example in Matlab:

```matlab
% Generate a random array of n 
% numbers between 0 and 99.
n = 9;
a = floor(rand(1, n) * 100);

disp(SMC(chart(a)));
disp(newline + mat2str(a)); 

function t = chart(a)
    m = 9;
    max_val = max(a);
    t = cell(m, length(a));

    for j = 0:(m-1)
        for i = 1:length(a)
            f = floor((m / max_val) * a(i));
            t{m-j, i} = char(9617); 
            if j < f
                t{m-j, i} = char(9619); 
            end
        end
    end
end

function r = SMC(a)
    [n, m] = size(a);
    r = '';

    for i = 1:(n+2)
        for j = 1:m

            if i <= n
                % Chart characters.
                r = [r a{i, j}];
            elseif i == (n+1)
                % Horizontal axis.
                r = [r '|'];
            else
                % Column numbers.
                r = [r num2str(j)];
            end
        end

        if i == (n+1)
            % Newline after the 
            % horizontal axis.
            r = [r newline];
        elseif i <= n
            % Row numbers 
            % and newline.
            r = [r '_' num2str(n-i+1) newline];
        end
    end
end
```

```text
Matlab output:

░░░░░░░▓░_9
░░░░░░░▓░_8
▓░░░░░░▓░_7
▓▓░░░░░▓▓_6
▓▓░░░░░▓▓_5
▓▓░░░░░▓▓_4
▓▓░░░░░▓▓_3
▓▓▓░░░░▓▓_2
▓▓▓▓▓░░▓▓_1
|||||||||
123456789

[85, 73, 25, 19, 13, 1, 5, 96, 73]
```

## References

- <i>Paul A. Gagniuc. Coding Examples from Simple to Complex - Applications in Python, Springer, 2024, pp. 1-245.</i>
- <i>Paul A. Gagniuc. Coding Examples from Simple to Complex - Applications in MATLAB, Springer, 2024, pp. 1-255.</i>
- <i>Paul A. Gagniuc. Coding Examples from Simple to Complex - Applications in Javascript, Springer, 2024, pp. 1-240.</i>

***
