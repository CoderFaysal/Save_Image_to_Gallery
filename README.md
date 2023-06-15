# Save Image to Gallery

```
private void saveImageToGallery() {
        // Get the Drawable from the ImageView
        Drawable drawable = full_images.getDrawable();

        // Convert the Drawable to a Bitmap
        Bitmap bitmap = ((BitmapDrawable) drawable).getBitmap();

        // Get the path to the external storage directory
        String path = Environment.getExternalStorageDirectory().toString();

        // Create a new directory in the external storage
        File dir = new File(path + "/Pictures");
        dir.mkdirs();

        // Create a file in the directory with a unique name
        String fileName = "image_" + System.currentTimeMillis() + ".jpg";
        File file = new File(dir, fileName);

        try {
            // Create an output stream to write the bitmap data to the file
            FileOutputStream outputStream = new FileOutputStream(file);

            // Compress the bitmap to JPEG format (you can change the format and quality as needed)
            bitmap.compress(Bitmap.CompressFormat.JPEG, 100, outputStream);

            // Flush and close the output stream
            outputStream.flush();
            outputStream.close();

            // Tell the media scanner to scan the new file
            MediaScannerConnection.scanFile(this, new String[]{file.getAbsolutePath()}, null, null);

            // Show a success message or any additional steps you want to perform
            Toast.makeText(this, "Image saved to gallery", Toast.LENGTH_SHORT).show();
        } catch (IOException e) {
            e.printStackTrace();
            // Show an error message or handle the exception as needed
            Toast.makeText(this, "Failed to save image", Toast.LENGTH_SHORT).show();
        }
    }
```
