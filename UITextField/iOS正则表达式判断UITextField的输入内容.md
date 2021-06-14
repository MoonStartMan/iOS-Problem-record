# iOS正则表达式判断UITextField的输入内容

## 1.限制输入框内只能是数字和字母(主要通过代理方法进行处理)

``` Objective-C

- (void)textFieldDidchange: (UITextField *)textField {
	NSString *textString = textField.text;
	if (![self inputShouldLetterOrNum: textString] && textString.length >0) {
		[HZKAlertTool alertMessage:@"只能是数字或者字母"];
		textField.text = self.currentText;
		return;
	}
	self.currentText = textString;
}

```

## 2.判断是否全是汉字

``` Objective-C

- (BOOL)inputShouldChineseWithText:(NSString *)inputString {
    if (inputString.length == 0) return NO;
    NSString *regex = @"[\u4e00-\u9fa5]+";
    NSPredicate *pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex];
    return [pred evaluateWithObject:inputString];
}

```

## 3.判断是否全数字

``` Objective-C

- (BOOL)inputShouldNumberWithText:(NSString *)inputString {
    if (inputString.length == 0) return NO;
    NSString *regex =@"[0-9]*";
    NSPredicate *pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex];
    return [pred evaluateWithObject:inputString];
}

```

## 4.判断是否全字母

``` Objective-C

- (BOOL)inputShouldLetterWithText:(NSString *)inputString {
    if (inputString.length == 0) return NO;
    NSString *regex =@"[a-zA-Z]*";
    NSPredicate *pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex];
    return [pred evaluateWithObject:inputString];
}

```

## 5.仅输入字母或数字

``` Objective-C

- (BOOL)inputShouldLetterOrNumWithText:(NSString *)inputString {
    if (inputString.length == 0) return NO;
    NSString *regex =@"[a-zA-Z0-9]*";
    NSPredicate *pred = [NSPredicate predicateWithFormat:@"SELF MATCHES %@",regex];
    return [pred evaluateWithObject:inputString];
}

```