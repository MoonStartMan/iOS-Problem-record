# 计算字体的Size


``` objective-c

UILabel *label = [[UILabel alloc]init];
label.text = @"labelText";
label.font = [UIFont systemFontOfSize: 10];
CGSize textSize = [label.text sizeWithAttributes:@{NSFontAttributeName:label.font}];

```