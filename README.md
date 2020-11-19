# Sequence diagrams

Diagrams have been created using [PlantUML](https://plantuml.com/).

If you want to contribute please read first the [documentation for sequence diagrams](https://plantuml.com/sequence-diagram) before updating/creating new diagrams in the `src/` directory.

## Install PlantUML

Download PlantUML compiled Jar from [https://plantuml.com/download](https://plantuml.com/download)

## Generate images from source

In the following we will assume that the sequence diagram source file is located at `./src/sequenceDiagram.plantml` and that we want to output the generated images direclty to the project base dir, which can be expressed as `..` relatively to where the source file is. We will also assume that `plantuml.jar` is in the project base dir, but you will need to update the commands with the actual path where you download it.

PlantUML supports exporting different images:

```text
    -tpng               To generate images using PNG format (default)
    -tsvg               To generate images using SVG format
    -teps               To generate images using EPS format
    -tpdf               To generate images using PDF format
    -tvdx               To generate images using VDX format
    -txmi               To generate XMI file for class diagram
    -tscxml             To generate SCXML file for state diagram
    -thtml              To generate HTML file for class diagram
    -ttxt               To generate images with ASCII art
    -tutxt              To generate images with ASCII art using Unicode characters
    -tlatex             To generate images using LaTeX/Tikz format
    -tlatex:nopreamble  To generate images using LaTeX/Tikz format without preamble
```

So you can just create a PNG from `./src/sequenceDiagram.plantml` in the project directory as:

```console
java -jar plantuml.jar -tpng -o .. ./src/sequenceDiagram.plantml
```

And for any other format just switch `-tpng` with the desired output format.

The case of pdf generation is somewhat special since the PlantUML export is, let's say it like this, not good, so it is preferable to export first to SVG with

```console
java -jar plantuml.jar -tsvg -o .. ./src/sequenceDiagram.plantml
```

and then use another software, such as [Inkscape](https://inkscape.org/), to create the PDF from the SVG.

You can do it manually or create a script.

In Linux/Mac, you can create a small one with filename `svgtopdf` with the following contents

```bash
#!/bin/bash
for file in "$@"; do
    inkscape --export-pdf="${file%.svg}.pdf" $file
done
```

Give your script execution permissions

```console
chmod +x svgtopdf
```

and move it somewhere in your path, for example to `/usr/local/bin`

```console
mv svgtopdf /usr/local/bin
```

No you can easily convert the SVG image to PDF with

```console
svgtopdf image.svg
```
