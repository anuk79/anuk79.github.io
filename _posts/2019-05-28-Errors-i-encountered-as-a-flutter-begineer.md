---
title:  "Errors I encountered as a Flutter beginner"
categories: flutter
tags: ['Flutter', 'Dart', 'Programming']
is_post: "True"
is_home_btn_reqd: "True"
subTitle: "In the coding universe, names matter a lot."
layout: default
permalink: /flutter/2019/05/28/errors-i-encountered-as-a-flutter-begineer/
prevBlogLink: /unit_tests/2019/05/18/how-should-i-unit-test-my-code-part-1/
nextBlogLink: /unit_tests/2019/06/22/how-should-i-unit-test-my-code-part-2/
is_project_btn_reqd: "False"
---



Hi everyone, today I will share some of the errors which I encountered while getting started with Flutter and how can we solve them. If you are already working with Flutter for sometime now, you might find the errors very naive and simple. But as a beginner in this new technology, with almost negligible prior experience in mobile development, it took time for me to research and fix these errors.
So it occurred to me, to create a list of the issues, to help anyone out there.

**Versions used**: Flutter 1.2.1 and Dart 2.1.2

Let’s get started…

## Error 1: flutter command not found

I followed the flutter setup for mac OS from the official website here.

The first issue that hit me was while adding path for Flutter in the bash profile. You can find the guidelines for this here. I followed the steps as mentioned, but still got the error ‘flutter command not found’ in the terminal while running command flutter doctor
This was due to missing out the leading ‘/’ while setting the path in bash profile. So, if you are someone who is getting this error, please go and cross-check the path first before looking out for more advanced troubleshooting.

PFB sample path:
`export PATH=”$PATH:/Users/anuradha.kumari/Documents/flutter/bin”`

## Error 2: Compiler cannot run without a compiler context

So, after fixing the first issue, I was all set to code my way through the first flutter app. 
I had two `.dart` files, main.dart and home_page.dart

And all I wanted was to set the `home` of my widget in main.dart file to be pointing to the widget as built from home_page.dart. 
So, I imported the home_page.dart file into the main.dart file and tried to hot reload the app. But alas! Only if life were that easy. Got the lengthy error in the terminal instead. Have a look:

```
  Internal problem: Compiler cannot run without a compiler context.
  Tip: Are calls to the compiler wrapped in CompilerContext.runInContext?
  #0      CompilerContext.current
  (package:front_end/src/fasta/compiler_context.dart:111:7)
  #1      internalProblem (package:front_end/src/fasta/problems.dart:45:25)
  #2      StackListener.checkEmpty
  (package:front_end/src/fasta/source/stack_listener.dart:184:7)
  <asynchronous suspension>
  .
  .
  .
  (dart:isolate/runtime/libisolate_patch.dart:172:5)
  Application finished.
```

To my good luck, I found the answer in the very first link of google search results. You can see it [here](https://github.com/flutter/flutter/issues/24964)

And the reason behind this seemingly long and complicated error message was use of double semicolons while importing my home_page.dart.

`import './home_page.dart';; //right here, double semicolon!!`

So, next time you run into such an issue, please double check for all your semi-colon usages. 
This is a compile time error and hence it also gets underlined in red, but when we are too busy finding issue in our code, we rarely look at the import statements (at least I did this mistake).

## Error 3: No Directionality widget found.

I was trying to work with widgets and I wanted to display a simple text in the center of the screen. 
But I did not want to use the `MaterialApp widget` for this. That’s it. Sounds simple, isn’t it.

To achieve that, I wrote below code:

```
  import 'package:flutter/material.dart';
  void main() => runApp(MyApp());
  class MyApp extends StatelessWidget {
    @override
    Widget build(BuildContext context) {
      return Container(
        child: Center(child: Text('my first app'))
      );
    }
  }
```

I restarted the app, and got below error in the terminal:

```
  flutter: ══╡ EXCEPTION CAUGHT BY WIDGETS LIBRARY ╞═══════════════════════════════════════════════════════════
  flutter: The following assertion was thrown building Text("my first app", dependencies: [DefaultTextStyle]):
  flutter: No Directionality widget found.
  flutter: RichText widgets require a Directionality widget ancestor.
  flutter: The specific widget that could not find a Directionality ancestor was:
  flutter:   RichText(softWrap: wrapping at box width, maxLines: unlimited, text: "my first app")
```

This error is a good one I must admit, since it gives me a hint to a probable fix. 
I searched for error and got good answers with explanation [here](https://stackoverflow.com/questions/49687181/no-directionality-widget-found) on stackoverflow.

The main reason here is that if we are not creating a **MaterialApp** widget (which provided the text direction as **LTR** by default), we need to specify explicitly the direction for **Text** widgets. 
Or alternatively, wrap them into the **Directionality** widget. In both cases, we will need to specify the **textDirection** property. My choice for fixing this issue was to specify the textDirection for Text widget itself. It solved the issue right away.

`Text('my first app', textDirection: TextDirection.ltr)`

These were the list of some issues which I hit into and felt like sharing with the broader audience so that it could help in easier debugging and troubleshooting.
As I continue to explore Flutter, let’s see what the future holds!

What issues did you face while learning Flutter? Do drop a comment if you feel like sharing.
Till then, happy learning, have a great day…

**Note**: Originally published [here](https://medium.com/@anuradha15/errors-i-encountered-as-a-flutter-beginner-8f4f75d82e5b)

<blockquote class="embedly-card" data-card-controls="0"><h4><a href="https://medium.com/@anuradha15/errors-i-encountered-as-a-flutter-beginner-8f4f75d82e5b">Errors I encountered as a Flutter beginner</a></h4><p>Hi everyone, today I will share some of the errors which I encountered while getting started with Flutter and how can we solve them. If you are already working with Flutter for sometime now, you might find the errors very naive and simple.</p></blockquote>
<script async src="//cdn.embedly.com/widgets/platform.js" charset="UTF-8"></script>
