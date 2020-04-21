# Learning Tesseract OCR

Notes during the learning process of [the Tesseract OCR engine](https://github.com/tesseract-ocr/tesseract).

## License

Unless otherwise specified, content in this work is release under the Creative Commons BY-SA 4.0+ license.  Most source materials are distributed under the Fair Use principle.

## Installation

This work is based on a self-built default variant of Tesseract 4.1.1, on a GNU/Linux operating system.

The recognition data used is [tessdata_best](https://github.com/tesseract-ocr/tessdata_best) commit [9e8aeef](https://github.com/tesseract-ocr/tessdata_best/commit/9e8aeef07ce8c4f6e6519577cee76363246bc6de), with the following SHA256 checksum:

```checksum
$ sha256sum *.traineddata
4fef2d1306c8e87616d4d3e4c6c67faf5d44be3342290cf8f2f0f6e3aa7e735b  chi_sim.traineddata
ea672a78157199c333aa12ec4e74550077689b545df5fc770903716850c8b2e5  chi_sim_vert.traineddata
1aa60488574cafa69486d919284f079ca9b68fcc7f6ad8dc1ff1b318dfd97028  chi_tra.traineddata
bbe518f94b9e3852109113507357bfe7e257834d88d2d1ead44178046bcd2181  chi_tra_vert.traineddata
8280aed0782fe27257a68ea10fe7ef324ca0f8d85bd2fd145d1c2b560bcb66ba  eng.traineddata
3af43a2420ce927dbce68474d644625947189a82ce6ae4fd32106399146819db  equ.traineddata
3a5291736537b6ed94e7e3064790788eba6deb517d5dd071005b2a2f57aa2339  HanS.traineddata
1ed0f838b85935d17a94a7ac6ca0194dc0cc099e9e6ce7112246ae7ab56b5b73  HanS_vert.traineddata
0de8b33fce2b03ef78ecc5ea4f5c699a218e4445bd05d532d305faa9f749e3cb  HanT.traineddata
4f4428a9e2368c5d58275f893dee60fafa1e8b8d96d9e16ee578f96387b1fca2  HanT_vert.traineddata
36bdf9ac823f5911e624c30d0553e890b8abc7c31a65b3ef14da943658c40b79  jpn.traineddata
1258be6eb2a9851f18043234ad18cca13ed32690bfff62b335c898bbea371548  jpn_vert.traineddata
9cf5d576fcc47564f11265841e5ca839001e7e6f38ff7f7aacf46d15a96b00ff  osd.traineddata

```

## Source materials

### UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS by 蔡英文(Ing-wen, Tsai)

Publically released full-text PDF, it is encrypted but should be decrypted easily.

## Single full text page OCR (to plaintext document) (English)

### Source material

From UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS, the material used is ACKNOWLEDGEMENT at page 7, it is extracted using the PDF Split and Merge Basic Editon software and is converted to PNG image using the `pdftoppm 'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf -png` command.

The resulting filename is [UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png>).

### Operation

```shell
tesseract \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png' \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png.ocr.eng._variant_' \
    -l eng
```

### Result(`tessdata_best` model)

[Quite perfect](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png.ocr.eng.tessdata_best.txt>), not a typo has been found.

### Result(`tessdata_fast` model)

[Also quite perfect](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_7.pdf.png.ocr.eng.tessdata_fast.txt>), the difference between the `tessdata_fast` model is that it recognizes wrong em-dash character.

## Single full text page OCR (to plaintext document) (Traditional Chinese)

### Source material

From UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS, the material used is "這本博士論文..." at page 2, it is extracted using the PDF Split and Merge Basic Editon software and is converted to PNG image using the `pdftoppm 'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf -png` command.

The resulting filename is [UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png>).

### Operation

```shell
tesseract \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png' \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr._variant_' \
    -l _lang_or_script_
```

### Result(`HanT` script; `tessdata_best` model)

[Suboptimal](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.HanT.tessdata_best.txt>), about 80% characters are correctly recognized, however some text is missing and most Han characters are unnecessarily splitted by a single space.

### Result(`HanT` script; `tessdata_fast` model)

[Suboptimal](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.HanT.tessdata_fast.txt>), about 80% characters are correctly recognized, IMO the `tessdata_best` model produces (very) slightly better result than this variant.

### Result(`chi_tra` script; `tessdata_best` model)

[Suboptimal](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.chi_tra.tessdata_best.txt>), about 80% characters are correctly recognized, however some text is missing and most Han characters are unnecessarily splitted by a single space.

Comparing with the result using `HanT` script this one is slightly better IMO.

### Result(`chi_tra` script; `tessdata_fast` model)

[Suboptimal](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.chi_tra.tessdata_fast.txt>), about 70% characters are correctly recognized, for some reason this testcase doesn't reproduce [Tesseract issue #2814](https://github.com/tesseract-ocr/tesseract/issues/2814).

### Result(`HanT` script; `tessdata_best` model; with workaround for [Tesseract issue #2814](https://github.com/tesseract-ocr/tesseract/issues/2814))

```shell
tesseract \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png' \
    'UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr._variant_' \
    -l _lang_or_script_ \
    -c preserve_interword_spaces=1
```

[Much better](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.HanT.tessdata_best.with_issue2814_workaround.txt>) than the one without the workaround.

### Result(`HanT` script; `tessdata_fast` model; with workaround for [Tesseract issue #2814](https://github.com/tesseract-ocr/tesseract/issues/2814))

[Slightly inferior](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.HanT.tessdata_fast.with_issue2814_workaround.txt>) than the `tessdata_best` counterpart.

### Result(`chi_tra` script; `tessdata_best` model; with workaround for [Tesseract issue #2814](https://github.com/tesseract-ocr/tesseract/issues/2814))

[Much better](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.chi_tra.tessdata_best.with_issue2814_workaround.txt>) than the one without the workaround.

### Result(`chi_tra` script; `tessdata_fast` model; with workaround for [Tesseract issue #2814](https://github.com/tesseract-ocr/tesseract/issues/2814))

[Inferior](<doc-assets/UNFAIR TRADE PRACTICES AND SAFEGUARD ACTIONS.decrypted.subset_2.pdf.png.ocr.chi_tra.tessdata_fast.with_issue2814_workaround.txt) than the `tessdata_best` counterpart.  About 60% of correctness.

## Reference

* [tesseract-ocr/tessdata_best: Best (most accurate) trained LSTM models.](https://github.com/tesseract-ocr/tessdata_best)
* [tesseract/tesseract.1.asc at tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract/blob/HEAD/doc/tesseract.1.asc#TESSDATADIR)
* [Chinese recognition was incorrectly segmented by spaces · Issue #2814 · tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract/issues/2814)
* [4.1.0 white list · Issue #2760 · tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract/issues/2760#issuecomment-560372382)