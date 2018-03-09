# pdf-ocr
node module that will do OCR on PDFs that do not contain text

## Inspired from pdf-extract
[https://www.npmjs.com/package/pdf-extract] by Noah Isaacson.  Many of the ideas initial design are from this project.

## Difference from pdf-extract
- Uses ES6 javascript
- using Promises instead of callbacks
- allows for extracting only the first page of the PDF to OCR (primary reason this was written for my own selfish reason!)
- does not do searchable PDFs.  Primary reason was it was next to impossible to get poppler instead on Windows. In the future I may add this
- if you need searchable PDFs, then I recommend using pdf-extract.

## Installation

`npm install pdf-ocr --save` 

After the installed, the following binaries need to be on in the path in order for the module to work.

### OSX

**pdftk**
[http://www.pdflabs.com/docs/install-pdftk/](http://www.pdflabs.com/docs/install-pdftk/)

- If you are installing on Siera or High Siera, you'll need to make sure you grab pdftk_server-2.02-mac_osx-10.11-setup.pkg
- Other versions, seemed to hang and not return any results.

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

For the OCR to work, you need to have the tesseract-ocr binaries available on your path. If you only need to handle ASCII characters, the accuracy of the OCR process can be increased by limiting the tesseract output. To do this copy the *alphanumeric* file included with this pdf-extract module into the *tess-data* folder on your system. Also the eng.traineddata included with the standard tesseract-ocr package is out of date. This pdf-extract module provides an up-to-date version which you should copy into the appropriate location on your system
``` bash
cd <root of this module>
cp "./share/eng.traineddata" "/usr/share/tesseract-ocr/tessdata/eng.traineddata"
cp "./share/configs/alphanumeric" "/usr/share/tesseract-ocr/tessdata/configs/alphanumeric"
```

### Windows
Important! You will have to add some variables to the PATH of your machine. You do this by right clicking your computer in file explorer, select Properties, select Advanced System Settings, Environment Variables. You can then add **the folder that contains the executables** to the path variable.

**pdftk** can be installed using the PDFtk Server installer found here: https://www.pdflabs.com/tools/pdftk-server/
It should autmatically add itself to the PATH, if not, the default install location is *"C:\Program Files (x86)\PDFtk Server\bin\"*

**ghostscript** for Windows can be found at: http://www.ghostscript.com/download/gsdnld.html
- Make sure you download the General Public License and the correct version (32/64bit).

- Install it and go to the installation folder (default: *"C:\Program Files\gs\gs9.19"*) and go into the **bin** folder.

- Rename the *gswin64c* to *gs*, and add the bin folder to your PATH.

**tesseract** can be build, but you can also download an older version which seems to work fine. Downloads at: https://sourceforge.net/projects/tesseract-ocr-alt/files/
Version tested is *tesseract-ocr-setup-3.02.02.exe*, the default install location is *"C:\Program Files (x86)\Tesseract-OCR"* and is also added to the PATH.
Note, this is only when you've checked that it will install for everyone on the machine.
