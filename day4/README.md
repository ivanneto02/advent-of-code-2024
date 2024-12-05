# Day 2

Final answer in Python:

## Part 1:

```python
# One thing to keep in mind is that we may capture a \n. This acts as a
# break between two rows. If I removed the \n, we would not have breaks and
# could potentially capture input from the next row.
def part1():

    txt = open("input.txt").read()
    length = txt.find("\n") + 1 # total line length, including \n
    rev = txt[::-1] # inverse
    count = 0

    # stride is 1 for forwards and backwards, length for up and down, length-1 for
    # left diagonal, length + 1 for right diagonal
    for stride in [1, length - 1, length, length + 1]:
        for i in range(len(txt) - stride*3):
            if txt[i:i+stride*3 + 1:stride] == "XMAS": count += 1 # forward
            if rev[i:i+stride*3 + 1:stride] == "XMAS": count += 1 # backward

    return count
```

## Part 2:

```python
# One thing to keep in mind is that we may capture a \n. This acts as a
# break between two rows. If I removed the \n, we would not have breaks and
# could potentially capture input from the next row.
def part2():

    txt = open("input.txt").read()
    length = txt.find("\n") + 1 # total line length, including \n
    count = 0

    # stride1 corresponds to moving down and right
    # stride2 corresponds to moving down and left
    stride1, stride2 = length+1, length-1

    # Grab the X for each char in txt
    for i in range(0, len(txt)):
        word1 = txt[i:i+stride1*2+1:stride1]      # top-down right diag
        word2 = txt[i+2:i+2+stride2*2+1:stride2]  # top-down left  diag
        
        if (("MAS" == word1) or ("SAM" == word1)) and \
           (("MAS" == word2) or ("SAM" == word2)):
            count += 1

    return count
```
Note: `txt[i:i+stride1*2+1:stride1]` starts at `i`, cuts `txt` until index `i+stride1*2+1   - 1` and iterates `stride1` from `i`. It will essentially move down and right twice to grab the word. Similarly, `txt[i+2:i+2+stride2*2+1:stride2]` does the same but starts at `i+1` and moves down and left twice to grab the word.
