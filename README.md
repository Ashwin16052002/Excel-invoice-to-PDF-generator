# 🧾 Excel Invoice to PDF Generator

A simple Python automation tool that converts **Excel invoice files into professionally structured PDF invoices**.

The application automatically reads Excel files from the `invoices` folder, extracts the invoice information and product details, calculates the total amount, and generates a corresponding PDF invoice inside the `PDFs` folder.

## ✨ Features

* 📊 Reads invoice data directly from Excel files
* 🧾 Automatically generates PDF invoices
* 📁 Supports batch processing of multiple Excel files
* 🔢 Extracts invoice number and date from the filename
* 📋 Creates a structured invoice table
* 💰 Automatically calculates the total invoice amount
* 📄 Generates A4-sized PDF documents
* ⚡ Simple command-line based automation
* 🐍 Built completely with Python

## 🛠️ Technologies Used

* **Python**
* **Pandas** – Reading and processing Excel data
* **OpenPyXL** – Excel file handling
* **FPDF** – PDF generation
* **Glob** – Finding invoice files
* **Pathlib** – File and path handling

The project's dependencies and pinned versions are defined in `requirements.txt`.

## 📂 Project Structure

```text
Excel-invoice-to-PDF-generator/
│
├── invoices/
│   └── invoice files (.xlsx)
│
├── PDFs/
│   └── generated PDF invoices
│
├── main.py
├── requirements.txt
├── README.md
└── .gitignore
```

## 📋 Excel File Format

The application expects the Excel workbook to contain a worksheet named:

```text
Sheet 1
```

The invoice data should contain the following columns:

| Column             | Description                      |
| ------------------ | -------------------------------- |
| `product_id`       | Unique identifier of the product |
| `product_name`     | Name of the product              |
| `amount_purchased` | Quantity purchased               |
| `price_per_unit`   | Price of one unit                |
| `total_price`      | Total price for the product      |

The program reads these values from each row and places them into the generated PDF invoice.

### Example

```text
product_id | product_name | amount_purchased | price_per_unit | total_price
-----------|--------------|------------------|----------------|------------
101        | Laptop       | 2                | 50000          | 100000
102        | Mouse        | 3                | 1000           | 3000
```

## 🗂️ Invoice File Naming

The Excel filename should follow this format:

```text
INVOICE_NUMBER-DATE.xlsx
```

### Example

```text
INV001-2026-09-21.xlsx
```

The application splits the filename using `-` and uses the resulting values as the invoice number and date.

## ⚙️ How It Works

```text
       Excel Invoice
            │
            ▼
     invoices/*.xlsx
            │
            ▼
       Read Excel
        using Pandas
            │
            ▼
    Extract Invoice Details
     ┌──────┴───────┐
     │              │
Invoice Number    Date
     │              │
     └──────┬───────┘
            ▼
      Read Product Data
            │
            ▼
     Calculate Total
            │
            ▼
      Generate A4 PDF
            │
            ▼
        PDFs/*.pdf
```

### 1. Find Excel Files

The program searches the `invoices` directory for Excel files:

```python
filepaths = glob.glob("invoices/*.xlsx")
```

### 2. Extract Invoice Information

The filename is used to extract the invoice number and date:

```python
filename = Path(filepath).stem
invoice_no, date = filename.split("-")
```

### 3. Read Excel Data

The program loads the `Sheet 1` worksheet using Pandas:

```python
df = pd.read_excel(filepath, sheet_name="Sheet 1")
```

### 4. Generate Invoice Table

The product information is written into the PDF, including:

* Product ID
* Product Name
* Quantity
* Price per Unit
* Total Price

### 5. Calculate Total

The total invoice amount is calculated from the `total_price` column:

```python
total_sum = df["total_price"].sum()
```

### 6. Generate PDF

The application creates an A4 PDF and saves it in the `PDFs` folder:

```python
pdf.output(f"PDFs/{filename}.pdf")
```

All of this processing is implemented in `main.py`.

## 🚀 Installation

### Prerequisites

Make sure Python 3.x is installed.

Check your Python version:

```bash
python --version
```

### Clone the Repository

```bash
git clone https://github.com/Ashwin16052002/Excel-invoice-to-PDF-generator.git
```

Navigate into the project:

```bash
cd Excel-invoice-to-PDF-generator
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

## ▶️ Usage

### Step 1 — Add Excel Files

Place your `.xlsx` invoice files inside:

```text
invoices/
```

### Step 2 — Run the Program

```bash
python main.py
```

### Step 3 — Check Generated PDFs

After successful execution, the generated invoices will be available inside:

```text
PDFs/
```

For example:

```text
PDFs/
├── INV001-2026-09-21.pdf
├── INV002-2026-09-21.pdf
└── INV003-2026-09-21.pdf
```

The application processes all matching Excel files found in the `invoices` directory.

## 📄 Generated PDF

Each generated invoice contains:

* Invoice number
* Invoice date
* Product information
* Quantity purchased
* Price per unit
* Total price for each product
* Overall invoice total

The PDF uses an A4 portrait layout and a table-based invoice format.

## 💡 Example Workflow

Suppose the `invoices` folder contains:

```text
invoices/
├── INV001-2026-09-21.xlsx
├── INV002-2026-09-21.xlsx
└── INV003-2026-09-21.xlsx
```

Run:

```bash
python main.py
```

The application automatically generates:

```text
PDFs/
├── INV001-2026-09-21.pdf
├── INV002-2026-09-21.pdf
└── INV003-2026-09-21.pdf
```

This makes the process useful when multiple invoices need to be converted without manually creating each PDF.

## 🔧 Customization

The PDF layout can be customized directly in `main.py`.

You can modify:

* Font family
* Font size
* Table column widths
* Text formatting
* PDF page layout
* Invoice fields
* Output location
* Invoice styling

For example, the current application uses the Times font and A4 portrait page format.

## ⚠️ Important Notes

For the current implementation to work correctly:

1. Excel files must have the `.xlsx` extension.
2. The worksheet must be named `Sheet 1`.
3. The required product columns must be present.
4. Invoice filenames must follow the expected `invoice-number-date` format.
5. The `PDFs` directory should be available for generated files.
6. The `total_price` column should contain numeric values.

## 🚀 Future Improvements

Possible improvements for future versions:

* [ ] Add a professional invoice template
* [ ] Add company name and logo
* [ ] Add customer information
* [ ] Add tax/GST calculation
* [ ] Add discounts
* [ ] Add currency formatting
* [ ] Add page numbers
* [ ] Add better error handling
* [ ] Validate Excel files before processing
* [ ] Automatically create the `PDFs` directory
* [ ] Add a graphical user interface
* [ ] Add email functionality for sending invoices
* [ ] Add customizable invoice templates
* [ ] Add logging and processing reports

## 📚 Use Cases

This project can be useful for:

* Small businesses
* Freelancers
* Retail businesses
* Sales teams
* Accounting workflows
* Automated billing systems
* Batch invoice generation
* Learning Python automation

## 👨‍💻 Author

**Ashwin V**

GitHub:
https://github.com/Ashwin16052002

LinkedIn:
https://www.linkedin.com/in/ashwin-v-5124992a9/

## 📜 License

This project is intended for educational and personal use.

---
