



## 算法题

[Integer to Roman](https://leetcode.com/submissions/detail/170013817/)

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

```c
void _1__9(int v, char *str, int *index_ptr, char _1, char _5, char _10) {
    // stupid but it works
    int i = *index_ptr;
    if (v == 1) {
        str[i++] = _1;
    } else if (v == 2) {
        str[i++] = _1;
        str[i++] = _1;
    } else if (v == 3) {
        str[i++] = _1;
        str[i++] = _1;
        str[i++] = _1;
    } else if (v == 4) {
        str[i++] = _1;
        str[i++] = _5;
    } else if (v == 5) {
        str[i++] = _5;
    } else if (v == 6) {
        str[i++] = _5;
        str[i++] = _1;
    } else if (v == 7) {
        str[i++] = _5;
        str[i++] = _1;
        str[i++] = _1;
    } else if (v == 8) {
        str[i++] = _5;
        str[i++] = _1;
        str[i++] = _1;
        str[i++] = _1;
    } else if (v == 9) {
        str[i++] = _1;
        str[i++] = _10;
    }
    *index_ptr = i;
}

char *intToRoman(int num) {
    // num is guaranteed to be [1, 3999]
    char ROMAN_ONE = 'I';
    char ROMAN_FIVE = 'V';
    char ROMAN_TEN = 'X';
    char ROMAN_FIFTY = 'L';
    char ROMAN_HUNDRED = 'C';
    char ROMAN_5_HUNDRED = 'D';
    char ROMAN_THOUSAND = 'M';
    char ROMAN_UNKNOWN = '-';
    
    char roman_nums[] = {
        ROMAN_ONE, 
        ROMAN_FIVE,
        ROMAN_TEN,
        ROMAN_FIFTY,
        ROMAN_HUNDRED,
        ROMAN_5_HUNDRED,
        ROMAN_THOUSAND,
        ROMAN_UNKNOWN, // placeholder
        ROMAN_UNKNOWN, // placeholder
    };
    int arabic_nums[] = {
        1, 5, 10, 50, 100, 500, 1000,
    };
    int i = sizeof(arabic_nums) / sizeof(int) - 1;
    int divider = arabic_nums[i];
    char *result = (char *)malloc(sizeof(char) * 100);
    int j = 0;
    while (num > 0 && divider > 0) {
        int quotient = num / divider;
        if (quotient > 0) {
            _1__9(quotient, result, &j, roman_nums[i], roman_nums[i+1], roman_nums[i+2]);
        }
        num = num % divider;
        i -= 2; // Why? @see arabic_nums = 1, 5, 10, 50, 100, 500, 1000, ...
        divider /= 10;
    }
    result[j++] = 0;
    return result;
}
```



## 知识点

### XPath

#### 概念

- Path 是 XSLT 标准中的主元素，可以用来定位 XML 文档中的元素和属性，用路径来表示（简化后）。
- 节点（Node）类型：元素（Element），属性（Attribute），文本（Text），命名空间（Namespace)，Processing-Instruction？？，注释（Comment）以及文档节点（Document Node）。
- XML 树形结构最顶层的元素被称为根元素（Root Element）。
- 没有子节点或父节点的节点为原子值（Atomic Value）。

```html
<bookstore>

<book>
  <title lang="en">Harry Potter</title>
  <price>29.99</price>
</book>

<book>
  <title lang="en">Learning XML</title>
  <price>39.95</price>
</book>

</bookstore>
```

| Expression | Description                                                  |
| ---------- | ------------------------------------------------------------ |
| *nodename* | Selects all nodes with the name "*nodename*"                 |
| /          | Selects from the root node                                   |
| //         | Selects nodes in the document from the current node that match the selection no matter where they are |
| .          | Selects the current node                                     |
| ..         | Selects the parent of the current node                       |
| @          | Selects attributes                                           |

| Path Expression | Result                                                       |
| --------------- | ------------------------------------------------------------ |
| bookstore       | Selects all nodes with the name "bookstore"                  |
| /bookstore      | Selects the root element bookstore**Note:** If the path starts with a slash ( / ) it always represents an absolute path to an element! |
| bookstore/book  | Selects all book elements that are children of bookstore     |
| //book          | Selects all book elements no matter where they are in the document |
| bookstore//book | Selects all book elements that are descendant of the bookstore element, no matter where they are under the bookstore element |
| //@lang         | Selects all attributes that are named lang                   |

| Path Expression                    | Result                                                       |
| ---------------------------------- | ------------------------------------------------------------ |
| /bookstore/book[1]                 | Selects the first book element that is the child of the bookstore element.**Note:** In IE 5,6,7,8,9 first node is[0], but according to W3C, it is [1]. To solve this problem in IE, set the SelectionLanguage to XPath:*In JavaScript: xml*.setProperty("SelectionLanguage","XPath"); |
| /bookstore/book[last()]            | Selects the last book element that is the child of the bookstore element |
| /bookstore/book[last()-1]          | Selects the last but one book element that is the child of the bookstore element |
| /bookstore/book[position()<3]      | Selects the first two book elements that are children of the bookstore element |
| //title[@lang]                     | Selects all the title elements that have an attribute named lang |
| //title[@lang='en']                | Selects all the title elements that have a "lang" attribute with a value of "en" |
| /bookstore/book[price>35.00]       | Selects all the book elements of the bookstore element that have a price element with a value greater than 35.00 |
| /bookstore/book[price>35.00]/title | Selects all the title elements of the book elements of the bookstore element that have a price element with a value greater than 35.00 |

| Wildcard | Description                  |
| -------- | ---------------------------- |
| *        | Matches any element node     |
| @*       | Matches any attribute node   |
| node()   | Matches any node of any kind |

| Path Expression | Result                                                       |
| --------------- | ------------------------------------------------------------ |
| /bookstore/*    | Selects all the child element nodes of the bookstore element |
| //*             | Selects all elements in the document                         |
| //title[@*]     | Selects all title elements which have at least one attribute of any kind |

| //book/title \| //book/price     | Selects all the title AND price elements of all book elements |
| -------------------------------- | ------------------------------------------------------------ |
| //title \| //price               | Selects all the title AND price elements in the document     |
| /bookstore/book/title \| //price | Selects all the title elements of the book element of the bookstore element AND all the price elements in the document |