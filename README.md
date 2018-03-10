# pdf-ocr
node module that will do OCR on PDFs that do not contain searchable text.

## Inspired from pdf-extract
[https://www.npmjs.com/package/pdf-extract] by Noah Isaacson.  Many of the ideas initial design are from this project.

## Difference from pdf-extract
- Uses ES6 javascript syntax.
- Uses Promises instead of callbacks
- Option to OCR just the first page of the PDF. (primary reason this was written for my own selfish reason!)
- Currently does not OCR searchable PDFs.  Plenty of options out there that does this.
- If you need to OCR searchable PDFs, I recommend using pdf-extract instead.

## Installation

`npm install pdf-ocr --save` 

After installing, the following binaries list below will need to be on your system as well as in the paths in your environment settings.

### OSX

**pdftk**
[http://www.pdflabs.com/docs/install-pdftk/](http://www.pdflabs.com/docs/install-pdftk/)

- If you're installing on OSX Sierra or High Sierra, you'll need to make sure you use pdftk_server-2.02-mac_osx-10.11-setup.pkg
- Other versions, seemed to hang the process.  If the tests fail, this could the main reason why.

**ghostscript**
``` bash
brew install gs
```

**tesseract** 

`brew install tesseract`

After tesseract is installed you need to install the alphanumeric config and an updated trained data file
``` bash
cd <root of this module>
cp "./share/eng.traineddata" "/usr/local/Cellar/tesseract/3.02.02_3/share/tessdata/eng.traineddata"
cp "./share/dia.traineddata" "/usr/local/Cellar/tesseract/3.02.02_3/share/tessdata/dia.traineddata"
cp "./share/configs/alphanumeric" "/usr/local/Cellar/tesseract/3.02.02_3/share/tessdata/configs/alphanumeric"
```

### Ubuntu
**pdftk**
```bash
apt-get install pdftk
```

**pdftotext**
``` bash
apt-get install poppler-utils
```

**ghostscript**
``` bash
apt-get install ghostscript
```

**tesseract**
``` bash
apt-get install tesseract-ocr
```

For the OCR to work, you need to have the tesseract-ocr binaries available on your path. If you only need to handle ASCII characters, the accuracy of the OCR process can be increased by limiting the tesseract output. To do this copy the *alphanumeric* file included with this module into the *tess-data* folder on your system. Also the eng.traineddata included with the standard tesseract-ocr package is out of date. This module provides an up-to-date version which you should copy into the appropriate location on your system.

``` bash
cd <root of this module>
cp "./share/eng.traineddata" "/usr/share/tesseract-ocr/tessdata/eng.traineddata"
cp "./share/configs/alphanumeric" "/usr/share/tesseract-ocr/tessdata/configs/alphanumeric"
```

### Windows

**pdftk** can be installed using the PDFtk Server installer found here: https://www.pdflabs.com/tools/pdftk-server/

**ghostscript** for Windows can be found at: http://www.ghostscript.com/download/gsdnld.html
- Make sure you download the General Public License and the correct version (32/64bit).

- Install it and go to the installation folder (default: *"C:\Program Files\gs\gs9.19"*) and go into the **bin** folder.

- Rename the *gswin64c* to *gs*, and add the bin folder to your PATH.

**tesseract**
- Download at: [https://sourceforge.net/projects/tesseract-ocr-alt/files/](https://sourceforge.net/projects/tesseract-ocr-alt/files/)

- *tesseract-ocr-setup-3.02.02.exe* is a version that I know works.
