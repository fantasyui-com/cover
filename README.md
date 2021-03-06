# mockup
Perspective app screens, and isometric mock-up designs.
Free Open Source automated high quality, high resolution, marketing art designer for mockup images.
Written in minimalist Bash using ImageMagick and Love!

This is a UNIX/Linux program first, you give it a screenshot of your program and it gives you that same screenshot carefully positioned in various scenarios, iPhone, TV, Laptop, etc... It exists because people and dribbbles keep bothering us about portfolios and we don't have time, the only time we do have is for a couple of commands, which is what mockup is great for.

![all](/docs/all.jpg)

## Installation

The current v2 is in development, it will be an rpm package, or now fork the repository, and use ./mockup

## Usage and Command Reference

### Image Based Templates

Output format is up to you, change hand1-demo.jpg to hand1-demo.png for PNG formatted image data.

```sh

mockup --template hand1 --input sample/image1.png --output hand1-demo.jpg

mockup --template laptop1 --input sample/image1.png --output laptop1-demo.jpg

mockup --template tablet1 --input sample/image1.png --output tablet1-demo.jpg

mockup --template tv1 --input sample/image1.png --output tv1-demo.jpg

```

### Synthetic/Generative Designs

Note the use of optional --background flag.

```sh

mockup --template stack2 --background '#002b36' --input sample/image1.png sample/image2.png --output stack2-demo.jpg

mockup --template stack3 --background '#002b36' --input sample/image1.png sample/image2.png sample/image3.png --output stack3-demo.jpg

```

### A Promise of Simplicity

KI.S.S., I will keep it sweet and simple, but we need dependency management to automatically install ImageMagick/GraphicsMagick, getopt and bc (and whatever else may come) to keep the dependency tree clean should the program be removed.

### Theory of Operation

1. Take royalty free source immage, add alpha (turn it into a standard png)
2. Punch a hole in it wherever there was a screen.
3. Now, take your image, distort it to fit that hole, layer the two, flatten the whole.
4. Export as jpg.
5. Upload it to your portfolio, blog, website, etc...

### Future Ahead

I wanted a simple an easy four point transform (aka. four point distort), but ImageMagick/GraphicsMagick seem to do exactly what we need, and come with extras that will help with slight image tweaks like desaturation, or adding noise. So, it makes no sense not to use those two.

### Programming Style

Bash is what it is, though I probably need to, I don't want to [generate argument parsing code](https://github.com/matejak/argbash), I want things to be plain and simple, I want the Bash to be redable.

#### 2.x The New Version

NOTE: Visit https://github.com/fantasyui-com/mockup/tree/v1 for the original sources.

I will provide an rpm that will include dependency handling and the next release will work like this

```shell


mockup --template laptop1 --output ~/the-result.png --input ~/Desktop/my-image1.png ~/Desktop/my-image2.png

mockup -t laptop1 -o ~/the-result.png -i ~/Desktop/my-image1.png ~/Desktop/my-image2.png

```

There maybe some interactive questions along the way if the user fails to name a valid template.

#### Bash 3 and Bash 4

I can't destroy the program because Apple is dragging behind, so I am going to aim for Bash 4, and use the new features to future proof the program.

#### Graphic GUI

It is possible to use Electron and ImageMagick/GraphicsMagick module, so that could be a neat experiment, but this is really meant to run on the command line, this is supposed to be a Juggernaut that takes a folder with screenshots and crunches through them to give you ready to use results. It is supposed to be done by the time programs like Electron begin starting up.

#### Graphic GUI Alternative: Raspberry PI

For people without a Linux computer. Microsoft and Apple make it difficult to publish software on their platforms, it will only get worse. On the Linux site, things only get better, it is a booming ecosystem of beautiful applications and powerful scripts.

I hope to create a simple way to install mockup on a $35 Raspberry PI, I will publish an article about the setup and use. And help you to your first Linux.

## Roadmap

- Each image will get a separate bash file (ex: mockup-tablet.sh, mockup-bigtv.sh) no more tv1 tv2.
- I would like the library of source images to be separated-out into mockup-library but it seems better to keep everything in one place for now.
- I will present a JSON pr easy to parse file, file for other languages implementations.


## Mockup Demos


hand1 preset
![hand1](/docs/hand1.jpg)

laptop1 preset
![laptop1](/docs/laptop1.jpg)

tablet1 preset
![tablet1](/docs/tablet1.jpg)

tv1 preset
![tv1](/docs/tv1.jpg)

### Synthetic/Generative

long1 preset
![long1](/docs/long1.jpg)

stack2 preset
![stack2](/docs/stack2.jpg)

stack3 preset
![stack3](/docs/stack3.jpg?)


Actual size close-up (resulting images are print quality)
![quality](/docs/quality.jpg)

## Requirements

- [ImageMagick](https://imagemagick.org)

## Quick Installation

    mkdir ~/GitHub; cd ~/GitHub;
    git clone git@github.com:fantasyui-com/mockup.git
    cd mockup;
    ./mockup --template hand1 --input Photos/face.jpg --output wow.jpg

## Bonus

Here is a quick script that will create images based on Screen*.png on your ~/Desktop (This may take a while). The program below is meant to help you get started on processing large collections.

```shell

#!/bin/bash
INDEX=1;
find ~/Desktop -maxdepth 1 -type f -iname "Screen*.png" | while read NAME
do
  mockup -t hand1 -i  "${NAME}" -o ./test-hand1-${INDEX}.png;
  mockup -t laptop1 -i  "${NAME}" -o ./test-laptop1-${INDEX}.png;
  mockup -t tv1 -i  "${NAME}" -o ./test-tv1-${INDEX}.png;
  mockup -t tablet1 -i  "${NAME}" -o ./test-tablet1-${INDEX}.png;
  INDEX=$((INDEX+1));
done;

```

## Changelog

- gray1 preset renamed to stack2
- added new preset stack3 for 3 images

## Credits

- [Alejandro Escamilla](https://unsplash.com/@alejandroescamilla)
  - [laptop1](https://unsplash.com/@alejandroescamilla?photo=xII7efH1G6o)
- [William Iven](https://unsplash.com/@firmbee)
  - [hand1](https://unsplash.com/@firmbee?photo=dAmHWsRYP9c)
  - [tablet1](https://unsplash.com/@firmbee?photo=GANqCr1BRTU)
- [Jens Kreuter](https://unsplash.com/@jenskreuter)
  - [tv1](https://unsplash.com/@jenskreuter?photo=ngMtsE5r9eI)
