# Barcode Inventory Management System

This Python script implements a real-time barcode inventory management system using a webcam. It utilizes OpenCV for video capture, `pyzbar` for barcode decoding, `sqlite3` for database management, and `threading` for concurrent barcode processing.

## Features

- Real-time barcode scanning using webcam.
- Automatic addition or subtraction of product quantities based on scanned barcodes.
- Persistent product information storage using SQLite.
- Multi-threaded queue-based processing for efficient barcode handling.
- Console interface for user interaction and input.

## Dependencies

Ensure the following Python libraries are installed:
- `opencv-python`
- `pyzbar`
- `sqlite3` (built-in with Python)
- `queue` and `threading` (built-in with Python)

Install required external libraries:
```bash
pip install opencv-python pyzbar
```

## Database Schema

A SQLite database named `barcode_data.db` is used with a single table `barcodes`:
- `sku` (TEXT, PRIMARY KEY): Barcode identifier.
- `quantity` (INTEGER): Inventory quantity.
- `product_name` (TEXT): Name of the product.
- `price` (REAL): Price of the product.

## Usage

1. **Run the Script**: The webcam will activate, and the interface will display the barcode scanner view.
2. **Scan a Barcode**: Hold a barcode in front of the camera to detect and display its SKU.
3. **Add Product**:
    - Press `a` to add quantity of detected SKU.
    - If SKU is new, you will be prompted to enter product name and price.
4. **Subtract Product**:
    - Press `s` to subtract quantity of detected SKU.
    - If quantity reaches zero, the product is removed from the database.
5. **Quit**:
    - Press `q` to exit the program.

## Threading and Queue

The script uses a separate thread (`process_barcodes`) to handle database updates for barcodes. Actions (`add` or `subtract`) are pushed to a `queue.Queue`, and the thread safely processes these in the background.

## Console Output

After each action, the script prints the current barcode inventory in a table format showing SKU, quantity, product name, and price.

## Example Output

```
Detected: SKU 123456789012
Added new product: SKU 123456789012 (Sample Product) to the database.

Current Barcode Data:
SKU       Quantity  Product Name        Price     
--------------------------------------------------
123456789012 1        Sample Product      9.99      
```

## Notes

- Reduce camera resolution for faster processing.
- Script ensures table schema consistency by checking for the `sku` column on startup.
- The script handles real-time image capture errors and ensures clean shutdown.

## License

This project is provided as-is for educational and prototyping purposes.
