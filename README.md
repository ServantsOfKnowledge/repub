### REPUB Features

REPUB is a comprehensive document processing pipeline that converts scanned book pages into high-quality, searchable digital documents. Key features include:

- **Image Processing**: Auto-cropping, deskewing and dewarping for scanned images
- **OCR Integration**: Multi-language text recognition using Tesseract
- **PDF Generation**: Creates searchable PDFs with embedded text layers
- **Command-line Tool**: For directly processing the scanned images into PDF, HOCR file and thumbnails 
- **Web Interface**: Django-based UI for job management and processing workflows along with a client that can submit jobs

## Quick Start

### Prerequisites

- Python 3.8+
- OpenCV
- Tesseract OCR
- Django 5.2
- PostgreSQL (for production)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd repub 
```

2. Install Python dependencies:
```bash
pip install -r requirements.txt
```

3. Install system dependencies:
```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr tesseract-ocr-all
sudo apt-get install poppler-utils

# macOS
brew install tesseract poppler
```
symlink repub in your site packages

```
ln -s <maindirectory>/repub <python_site_package_dir>/repub
```

## REPUB Usage

### Command Line Processing

The `process_raw.py` tool provides direct command-line access to the document processing pipeline:

#### Basic Usage

```bash
cd repub/

# Process images from a directory
python process_raw.py -i input_directory -o output_directory --crop --deskew --ocr

# Process a PDF file
python process_raw.py -I input.pdf -O output.pdf --crop --deskew --ocr

# Create Internet Archive compatible output
python process_raw.py -i input_directory -A ia_output_directory
```

#### Common Options

| Option | Description |
|--------|-------------|
| `-i, --indir` | Input directory containing scanned images |
| `-I, --inpdf` | Input PDF file to process |
| `-o, --outdir` | Output directory for processed images |
| `-O, --outpdf` | Output PDF file path |
| `-A, --iadir` | Internet Archive format output directory |
| `-c, --crop` | Auto-crop page boundaries |
| `-D, --deskew` | Detect and correct page skew |
| `-t, --ocr` | Perform OCR and create searchable PDF |
| `-L, --language` | OCR language (default: eng) |
| `-r, --reduce` | Scale images by factor (e.g., 0.5 for 50%) |
| `-w, --dewarp` | Apply dewarping to curved pages |
| `-m, --maxcontours` | Max contours for cropping analysis (default: 5) |


### Web Interface (RepubUI)

The Django-based web interface provides a user-friendly way to manage document processing jobs:

#### Setup

1. Navigate to the web application directory:
```bash
cd repubui/
```

2. Configure environment variables:
```bash
# Create .env file
cp .env.example .env
# Edit .env with your settings
```

3. Set up the database:
```bash
python manage.py makemigrations
python manage.py migrate
```

4. Create a superuser account:
```bash
python manage.py createsuperuser
```

5. Start the development server:
```bash
python manage.py runserver
```

#### Web Interface Features

- **Job Management**: Upload, monitor, and manage processing jobs
- **Page-by-Page Review**: Individual page editing and adjustment
- **Batch Processing**: Handle multiple documents simultaneously
- **Admin Interface**: User management and system configuration
- **API Access**: RESTful API for programmatic access

#### Access Points

- **Main Interface**: http://localhost:8000/
- **Admin Panel**: http://localhost:8000/admin/
- **API Documentation**: http://localhost:8000/api/


