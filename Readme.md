# WooCommerce to Zoho CRM Integration using Deluge

This project provides a complete, step-by-step guide to automatically integrate a local WooCommerce store with Zoho CRM. The integration uses a Zoho Deluge script to fetch new customer orders and create corresponding Contacts, Products, and Deals within Zoho CRM.

## 🎯 Objective

The goal is to build an automated workflow that sends customer and order data from a WooCommerce store into Zoho CRM. For each new order, the script will:

1.  Create (or find) a **Contact** for the customer.
2.  Create (or find) the **Products** from the order.
3.  Create a new **Deal** with the order details.
4.  Associate the Contact and Products with the newly created Deal.

## ✨ Features

-   **Automated Data Sync**: Runs on a schedule to fetch the latest orders.
-   **Contact Management**: Creates new contacts or uses existing ones based on the customer's email.
-   **Product Management**: Creates new products in Zoho CRM if they don't already exist.
-   **Sales Pipeline Automation**: Automatically creates deals from new orders, populating them with the order total and associating them with the correct contact and products.
-   **Duplicate Prevention**: Checks for existing deals to avoid creating duplicates for the same order.
-   **Serverless**: The entire automation logic runs within Zoho's infrastructure using Deluge, requiring no separate server.

## 🛠️ Requirements

-   A local WordPress installation.
-   **[LocalWP](https://localwp.com/)**: A free WordPress development tool. We will use its **Live Link** feature to expose the local site to the internet temporarily.
-   **[WooCommerce](https://woocommerce.com/)** plugin for WordPress.
-   A **[Zoho CRM](https://www.zoho.com/crm/)** account (a Zoho One free trial works perfectly).

---

## 🚀 Setup Instructions

Follow these steps carefully to set up the integration.

### Step 1: Prepare Your WooCommerce Environment

First, set up your local store and populate it with test data.

1.  **Install LocalWP**: Download and install the application from the official website.
2.  **Create a WordPress Site**: Launch LocalWP and create a new local website.
3.  **Install WooCommerce**: Log in to your new WordPress admin dashboard, navigate to **Plugins > Add New**, search for "WooCommerce," and then install and activate it.
4.  **Add Sample Products**: Go to **Products > Add New** and create at least 3 sample products.
5.  **Place Test Orders**: Visit your local store's frontend, add products to the cart, and complete the checkout process as a dummy customer. Place at least 2 test orders.

### Step 2: Activate and Use LocalWP's Live Link

For Zoho's servers to communicate with your local store, you must make it accessible online.

1.  In the LocalWP application, with your site running, find the **"Live Link"** button at the top and click **"Enable"**.
2.  LocalWP will generate a publicly accessible URL (e.g., `https://random-name.loca.lt`) and provide a username and password.
3.  **Keep this Live Link active** whenever you want the integration to run. Note down the **URL, username, and password**, as they will be needed for your script.

### Step 3: Configure WooCommerce REST API

Generate API keys in WooCommerce to grant the script access to your store's data.

1.  In your WordPress dashboard, go to **WooCommerce > Settings > Advanced > REST API**.
2.  Click **"Add key"**.
3.  Give the key a **Description** (e.g., "Zoho CRM Sync").
4.  Set the **Permissions** to **"Read/Write"**.
5.  Click **"Generate API key"**.
6.  **Important**: Copy the **Consumer key** and **Consumer secret** immediately and save them somewhere safe. You will need them for the script.

### Step 4: Create the Zoho Deluge Function

Now, set up the function in Zoho CRM where your code will live.

1.  Log in to your Zoho CRM account.
2.  Click the **gear icon** (Settings) in the top right.
3.  Navigate to **Developer Space > Functions**.
4.  Click **New Function**.
5.  Enter the following details:
    -   **Function Name**: `fetchWooCommerceOrders`
    -   **Display Name**: Fetch WooCommerce Orders
    -   **Category**: Automation
6.  Click **Create**.

### Step 5: Implement the Deluge Script

1.  Open the newly created Deluge function editor.
2.  Paste the Deluge script (fetchWooCommerceOrders.dg) into the editor.
3.  Carefully update the placeholder variables at the top of the script with your unique credentials:
    -   `local_username`
    -   `local_password`
    -   `wc_base_url` (using your Live Link URL)
    -   `consumer_key`
    -   `consumer_secret`
4.  Click **Save** to save the function.

### Step 6: Testing and Verification

1.  Ensure your site is running in LocalWP and the **Live Link is active**.
2.  Place a **new test order** on your WooCommerce store using the Live Link URL.
3.  Go to the Deluge function editor in Zoho CRM and click **"Save and Execute"** to run the script immediately.
4.  Check the console at the bottom for any `info` or `Error` messages.
5.  **Verify in Zoho CRM**:
    -   Navigate to the **Contacts** module. You should see the new customer.
    -   Navigate to the **Products** module. You should see any new products from the order.
    -   Navigate to the **Deals** module. You should see the new deal, linked to the correct contact and products.