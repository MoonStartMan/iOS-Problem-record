# indexPath.row 转换为数字,以及转换为"A,B,C,D"

## indexPath.row转换为数字

``` Objective-C

[NSString stringWithFormat: @"%ld", indexPath.row];

```

## indexPath.row转换为"A,B,C,D"

``` Objective-C

[NSString stringWithFormat: @"%c", (char)('A' + indexPath.row)];

```