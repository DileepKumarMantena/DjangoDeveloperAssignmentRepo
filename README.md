# Vendor and Purchase Order Management System

This Django application provides a management system for vendors and purchase orders. It includes models for vendors, purchase orders, and historical performance metrics, along with a set of CRUD APIs for managing these entities.

## Table of Contents

- [Getting Started](#getting-started)
- [Models](#models)
  - [Vendor_Model](#vendor_model)
  - [PurchaseOrder](#purchaseorder)
  - [HistoricalPerformance](#historicalperformance)
- [API Endpoints](#api-endpoints)
  - [Vendor Endpoints](#vendor-endpoints)
  - [Purchase Order Endpoints](#purchase-order-endpoints)
- [Setup and Installation](#setup-and-installation)
  - [MySQL Database Setup](#mysql-database-setup)
  - [Environment Configuration](#environment-configuration)
  - [Running the Application](#running-the-application)
- [Usage](#usage)

## Getting Started

To get started with this project, you will need to have Python and Django installed on your machine. Follow the setup instructions below to get the application running.

## Models

### Vendor_Model

Represents a vendor with the following fields:

- `name`: CharField, maximum length 255
- `contact_details`: TextField
- `address`: TextField
- `vendor_code`: CharField, maximum length 50, unique
- `on_time_delivery_rate`: FloatField
- `quality_rating_avg`: FloatField
- `average_response_time`: FloatField
- `fulfillment_rate`: FloatField

### PurchaseOrder

Represents a purchase order with the following fields:

- `po_number`: CharField, maximum length 50, unique
- `vendor`: ForeignKey to Vendor_Model
- `order_date`: DateTimeField
- `delivery_date`: DateTimeField
- `items`: JSONField
- `quantity`: IntegerField
- `status`: CharField, maximum length 50
- `quality_rating`: FloatField, null=True, blank=True
- `issue_date`: DateTimeField
- `acknowledgment_date`: DateTimeField, null=True, blank=True

### HistoricalPerformance

Represents the historical performance of a vendor with the following fields:

- `vendor`: ForeignKey to Vendor_Model
- `date`: DateTimeField
- `on_time_delivery_rate`: FloatField
- `quality_rating_avg`: FloatField
- `average_response_time`: FloatField
- `fulfillment_rate`: FloatField

## API Endpoints

### Vendor Endpoints

- `POST /vendors/CreatingNewVendor/`: Create a new vendor
- `GET /vendors/GetAllVendorsListApi/`: Get a list of all vendors
- `GET /vendors/GetVendorsDetailsById/<int:id>/`: Get details of a vendor by ID
- `PUT /vendors/UpdateVendorsDetailsById/<int:id>/`: Update details of a vendor by ID
- `DELETE /vendors/DeleteVendorsDetails/<int:id>/`: Delete a vendor by ID
- `GET /vendors/GetVendorPerformanceApi<int:id>/`: Get vendor performance by ID

### Purchase Order Endpoints

- `POST /purchase-orders/CreateNewPurchaseOrderApi/`: Create a new purchase order
- `GET /purchase-orders/GetPurchaseDetailsById/<int:id>/`: Get purchase order details by ID
- `GET /purchase-orders/GetPurchaseDetailsByVendorId/<int:vendor>/`: Get purchase order details by vendor ID
- `DELETE /purchase-orders/DeletePurchaseOrderDetails/<int:id>/`: Delete a purchase order by ID
- `PUT /purchase-orders/UpdatePurchaseOrdersById<int:id>/`: Update purchase order by ID
- `POST /purchase-orders/api/purchase_orders/<int:id>/acknowledge`: Acknowledge a purchase order

## Setup and Installation

### MySQL Database Setup

1. **Install MySQL:**
   Download and install MySQL from the official website: [MySQL Downloads](https://dev.mysql.com/downloads/). Follow the installation instructions specific to your operating system.

2. **Create a Database:**
   After installing MySQL, you need to create a database for your Django application.
   ```sh
   mysql -u root -p
   CREATE DATABASE DjangoDatabase;
   ```


### Environment Configuration

1. **Clone the repository:**
   ```sh
   git clone https://github.com/your-username/vendor-purchase-order-management.git
   cd vendor-purchase-order-management
   ```

2. **Create a virtual environment:**
   ```sh
   python -m venv venv
   source venv/bin/activate  # On Windows use `venv\Scripts\activate`
   ```

3. **Install the dependencies:**
   ```sh
   pip install -r requirements.txt
   ```

4. **Update `settings.py` with your database configuration:**
   Open the `settings.py` file and configure the `DATABASES` setting as follows:
   ```python
   DATABASES = {
       'default': {
           'ENGINE': 'django.db.backends.mysql',
           'NAME': 'DjangoDatabase',        # Name of your database
           'USER': 'django_user',           # Your MySQL user
           'PASSWORD': 'your_password',     # Your MySQL user's password
           'HOST': 'localhost',             # Or the IP address of your MySQL server
           'PORT': '3306',                  # Default MySQL port
       }
   }
   ```

5. **Install MySQL client for Python:**
   To connect Django to MySQL, you need to install the MySQL client library.
   ```sh
   pip install mysqlclient
   ```

### Running the Application

1. **Apply migrations:**
   Django uses migrations to propagate changes you make to your models (adding a field, deleting a model, etc.) into your database schema. Run the following command to apply migrations:
   ```sh
   python manage.py migrate
   ```

2. **Create a superuser (Admin user):**
   Create a superuser to access the Django admin interface.
   ```sh
   python manage.py createsuperuser
   ```

3. **Run the development server:**
   Start the Django development server to serve your application.
   ```sh
   python manage.py runserver
   ```

4. **Access the application:**
   Open your web browser and navigate to `http://localhost:8000`. You should see your Django application running.

5. **Access the admin interface:**
   Navigate to `http://localhost:8000/admin` and log in with the superuser credentials you created earlier to manage your models through the admin interface.

## Usage

Follow the above steps to set up and run your Django application. Ensure your MySQL server is running and properly configured to allow connections from your Django application. The detailed instructions should help you troubleshoot any issues related to the database connection and running the app.
```

This expanded version provides comprehensive guidance on setting up and configuring the MySQL database, updating the Django settings, applying migrations, creating a superuser, and running the application.
