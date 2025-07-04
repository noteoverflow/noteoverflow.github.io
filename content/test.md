+++
title = "Test"
date = 2000-01-01
extra.katex = true
+++

## 繁体中文测试
This is a chinese test post to show you how chinese is displayed.

善我王上魚、產生資西員合兒臉趣論。畫衣生這著爸毛親可時，安程幾？合學作。觀經而作建。都非子作這！法如言子你關！手師也。

以也座論頭室業放。要車時地變此親不老高小是統習直麼調未，行年香一？

就竟在，是我童示讓利分和異種百路關母信過明驗有個歷洋中前合著區亮風值新底車有正結，進快保的行戰從：弟除文辦條國備當來際年每小腳識世可的的外的廣下歌洲保輪市果底天影；全氣具些回童但倒影發狀在示，數上學大法很，如要我……月品大供這起服滿老？應學傳者國：山式排只不之然清同關；細車是！停屋常間又，資畫領生，相們制在？公別的人寫教資夠。資再我我！只臉夫藝量不路政吃息緊回力之；兒足灣電空時局我怎初安。意今一子區首者微陸現際安除發連由子由而走學體區園我車當會，經時取頭，嚴了新科同？很夫營動通打，出和導一樂，查旅他。坐是收外子發物北看蘭戰坐車身做可來。道就學務。

國新故。

> 这群在连云港过冬的蛎鹬本来依赖两个因放水而露出底部的鱼塘作为高潮栖息地，但是前段时间鱼塘又开始蓄水，让它们失去了合适的高潮地，潮水上涨时候只能像这样挤在鱼塘边的土质堤坝上，休息环境更差而且容易受人惊扰，实在是很可怜

> 工步他始能詩的，裝進分星海演意學值例道……於財型目古香亮自和這乎？化經溫詩。只賽嚴大一主價世哥受的沒有中年即病行金拉麼河。主小路了種就小為廣不？

## 日本語テスト
This is a Japanese test post to show you how japanese is displayed.

私は昨日ついにその助力家というのの上よりするたなけれ。 最も今をお話団はちょうどこの前後なかろでくらいに困りがいるたをは帰着考えたなかって、そうにもするでうたらない。 がたを知っないはずも同時に九月をいよいよたありた。

もっと槙さんにぼんやり金少し説明にえた自分大した人私か影響にというお関係たうませないが、この次第も私か兄具合に使うて、槙さんののに当人のあなたにさぞご意味と行くて私個人が小尊敬を聴いように同時に同反抗に集っだうて、いよいよまず相当へあっうからいだ事をしでなけれ。

> それでそれでもご時日をしはずはたったいやと突き抜けるますて、その元がは行ったてという獄を尽すていけですた。

## 简体中文测试
效育声去本义然空，各值太法心想，场强实地。 题铁习点儿表管少间千，只何政亲织文意部，千影画派证男须。 手反取长风治增非等直难群，连取及天他己事头级，影数弦适把气快目人。 专议以省通引而千个，格则口段度样水热马，地教少务改磨。 包思外心半院应她算斯，市外会快记路又火学，劳如肃它准众丧边。

> 团算部住县单总边素格军所，合音府教看和广光采率位转，位用品根确针百。 证其标元角工方海接交他，论象切万世认一响义，治然身本风弦带题。 向我次路持加北，她不反心。 说总元军例市决，现始即算证养，规走还壳。


## H2

### H3

- 1

1. 2

## font

testing: `code`

testing: *italic*

testing: **bold**

## mathjax

\\( \int x dx = \frac{x^2}{2} + C \\)

\\[ \mu = \frac{1}{N} \sum_{i=0} x_i \\]

## katex

testing: inline formula: $\int_a^b f(x) dx = F(b) - F(a)$

testing: block formula: $$f g = g f g$$

$$
\int_0^1x^4 \sqrt{\frac {1+x} {1-x}}dx
$$

$$
\lim f(x) - g(x) = g(x) (\frac {f} {g} - 1)
$$

## code

### C++
```cpp
#include __FILE__

template <typename T, class C, int R>
using T = C<R>;

static inline register void main(){
    auto f = main();
    int a = (long) (void*) &f;
    f(a);

    return 1;
}
```

### Rust
```rust
fn longer<'a, 'b, 'c>(a: &'a str, b: &'b str) -> &'c str
where
    'a: 'c,
    'b: 'c,
{
    if a.len() < b.len() {
        b
    } else {
        a
    }
}
```

### Haskell
```haskell
primes = filterPrime [2..] where
    filterPrime (p:xs) =
        p : filterPrime [x | x <- xs, x `mod` p /= 0]
```