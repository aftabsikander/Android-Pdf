# ReadPDF
Read, render and view PDF with Android L's PdfRenderer.
The app render PDF to Bitmap which is viewed as a imageView.

Uses android.graphics.pdf.PdfRenderer
https://developer.android.com/preview/api-overview.html
### Features
Previous/Next Page - Navigate through pages with next and previous buttons.
### Missing
Ability to zoom and select text.
## Usage
Please download test.pdf to the default Download folder with either adb or web browser. In newer cases, this would make the pdf's absolute url /sdcard/Download/test.pdf.
### Code
```
imageView = (ImageView) findViewById(R.id.imageView);`
Bitmap bitmap = Bitmap.createBitmap(500, 500, Bitmap.Config.ARGB_4444);

try {
    File file = new File("/sdcard/Download/test.pdf");
    PdfRenderer renderer = new PdfRenderer(ParcelFileDescriptor.open(file, ParcelFileDescriptor.MODE_READ_ONLY));

    if(currentPage<0){
      currentPage = 0;
    }else if(currentPage > renderer.getPageCount()){
      currentPage = renderer.getPageCount()-1;
    }

    renderer.openPage(currentPage).render(bitmap, new Rect(0, 0, 500, 500), new Matrix(), PdfRenderer.Page.RENDER_MODE_FOR_DISPLAY);
    imageView.setImageBitmap(bitmap);
    imageView.invalidate();
```

## Screenshot
![alt text](https://github.com/digipost/android-pdf/blob/master/screenshot.png "Screenshot")

## License
Apache License, Version 2.0