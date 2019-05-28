```objc 

#import "ViewController.h"
#import <CoreText/CoreText.h>
@interface ViewController ()

@property (strong, nonatomic) UILabel *label;

@property (strong, nonatomic) UILabel *MuTabelLabel;

@end

@implementation ViewController

- (void)viewDidLoad {
[super viewDidLoad];

/*----------------------------------------设置Label基本属性------------------------------------------------------*/

### 初始化，设置坐标
self.label = [[UILabel alloc] initWithFrame:CGRectMake(25, 200, 325, 100)];

//设置Label文字
self.label.text = @"今天天气真冷，天气又要降温了，大家要注意保暖啊";

//设置Label文字格式（居中对齐等）
self.label.textAlignment = NSTextAlignmentCenter;

//设置Label的行数（默认是1）
self.label.numberOfLines = 2;

//设置Label文字颜色
self.label.textColor = [UIColor orangeColor];

//设置Label的背景颜色
self.label.backgroundColor = [UIColor grayColor];

//设置Label的文字的阴影颜色
self.label.shadowColor = [UIColor cyanColor];

//设置Label文字的阴影部分的偏移量
self.label.shadowOffset = CGSizeMake(5, 30);

//默认是NSLineBreakByTruncatingTail。用于单和多行文本
self.label.lineBreakMode = NSLineBreakByTruncatingTail;
/*
NSLineBreakByWordWrapping = 0,//以空格为边界，保留单词 (包装在单词边界)
NSLineBreakByCharWrapping,    //保留整个字符 (包装在字符边界)
NSLineBreakByClipping,        //简单剪裁，到边界为止
NSLineBreakByTruncatingHead,  //按照"……文字"显示
NSLineBreakByTruncatingTail,  //按照"文字……"显示
NSLineBreakByTruncatingMiddle //按照"文字……文字"显示
*/

//启用用户交互（触发touchBegan）
self.label.userInteractionEnabled = YES;

//更改标签如何绘制（默认是YES）
self.label.enabled = YES;

/*--------------------------------设置Label自动版式，属性文本的设置----------------------------------------------*/

//属性字符串
NSMutableAttributedString *String = [[NSMutableAttributedString alloc] initWithString:@"忽如一夜春风来，千树万树梨花开"];

//设置属性字符串的字体大小（方法1）add方法
[String addAttribute:NSFontAttributeName value:[UIFont systemFontOfSize:12] range:NSMakeRange(3, 4)];

//设置属性字符串的颜色（方法2）set方法
[String setAttributes:[NSDictionary dictionaryWithObjectsAndKeys:[UIColor redColor],NSForegroundColorAttributeName,nil] range:NSMakeRange(0, 4)];

//设置属性字符串的下划线样式，需要导入<CoreText/CoreText.h>头文件
[String addAttribute:(NSString *)kCTUnderlineStyleAttributeName value:(id)[NSNumber numberWithInt:kCTUnderlineStyleDouble] range:NSMakeRange(0, 9)];

//初始化一个新的Label
self.MuTabelLabel = [[UILabel alloc] initWithFrame:CGRectMake(25, 400, 325, 100)];
self.MuTabelLabel.backgroundColor = [UIColor cyanColor];

//给Label添加属性文本
self.MuTabelLabel.attributedText = String;

//设置对齐基线，默认是否定的。如果是的,文本将缩小minFontSize基线
self.MuTabelLabel.adjustsFontSizeToFitWidth = YES;
/*  UIBaselineAdjustmentAlignBaselines //文本最上端与Label中线对齐，默认值
UIBaselineAdjustmentAlignCenters   //文本中线与Label中线对齐
UIBaselineAdjustmentNone           //文本最下端与Label中线对齐
*/

//UILabel接受的最小字体
self.MuTabelLabel.minimumScaleFactor = 12;

//当父试图的interaction置为NO，子控件，子试图的也不会触发
self.view.userInteractionEnabled = YES;

/*-------------------------------添加到视图---------------------------------------------*/

//加载到视图中
//    [self.view addSubview:self.label];

[self.view addSubview:self.MuTabelLabel];
}

//响应者链 ：如果父试图的userInteractionEnable置为NO，那么子试图变无法响应（响应者链的原理）
- (void)touchesBegan:(NSSet *)touches withEvent:(UIEvent *)event
{
NSLog(@"%@",[touches valueForKey:@"view"]);
}



- (void)didReceiveMemoryWarning {
[super didReceiveMemoryWarning];
// Dispose of any resources that can be recreated.
}

@end

```
