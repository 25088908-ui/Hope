# main.java
Main java

    }

    public void CaptureProduct() {
        System.out.println("\nCAPTURE A NEW PRODUCT");
        System.out.println("*********************");
        
        System.out.print("Enter the product code: ");
        String code = scanner.nextLine();
        
        System.out.print("Enter the product name: ");
        String name = scanner.nextLine();

        String category = "";
        while (true) {
            System.out.println("Select the product category:");
            System.out.println("Desktop Computer - 1");
            System.out.println("Laptop - 2");
            System.out.println("Tablet - 3");
            System.out.println("Printer - 4");
            System.out.println("Gaming Console - 5");
            System.out.print("Product Category >> ");
            String catInput = scanner.nextLine();

            if (catInput.equals("1")) { category = "Desktop Computer"; break; }
            else if (catInput.equals("2")) { category = "Laptop"; break; }
            else if (catInput.equals("3")) { category = "Tablet"; break; }
            else if (catInput.equals("4")) { category = "Printer"; break; }
            else if (catInput.equals("5")) { category = "Gaming Console"; break; }
            else {
                System.out.println("Invalid entry! Please select a valid category option.");
            }
        }

        System.out.print("Indicate the product warranty. Enter (1) for 6 months or any other key for 2 years: ");
        String warrantyInput = scanner.nextLine();
        String warranty = warrantyInput.equals("1") ? "6 months" : "2 years";

        double price = 0;
        while (true) {
            try {
                System.out.print("Enter the price for " + name + " >> ");
                price = Double.parseDouble(scanner.nextLine());
                break;
            } catch (NumberFormatException e) {
                System.out.println("Invalid amount. Please enter a valid decimal number.");
            }
        }

        int stock = 0;
        while (true) {
            try {
                System.out.print("Enter the stock level for " + name + " >> ");
                stock = Integer.parseInt(scanner.nextLine());
                break;
            } catch (NumberFormatException e) {
                System.out.println("Invalid stock level. Please enter a whole integer.");
            }
        }

        System.out.print("Enter the supplier for " + name + " >> ");
        String supplier = scanner.nextLine();

        ReportData newProduct = new ReportData(code, name, category, warranty, price, stock, supplier);
        SaveProduct(newProduct);
    }

    public void SaveProduct(ReportData product) {
        productList.add(product);
        System.out.println("Product details have been saved successfully!!!");
    }

    public void SearchProduct() {
        System.out.print("\nPlease enter the product code to search: ");
        String code = scanner.nextLine();
        System.out.println("*******************************************************************");
        System.out.println("PRODUCT SEARCH RESULTS");
        System.out.println("*******************************************************************");

        ReportData found = findProductByCode(code);
        if (found != null) {
            System.out.println("PRODUCT CODE:\t\t" + found.getProductCode());
            System.out.println("PRODUCT NAME:\t\t" + found.getProductName());
            System.out.println("PRODUCT WARRANTY:\t" + found.getProductName());
            System.out.println("PRODUCT CATEGORY:\t" + found.getProductCategory());
            System.out.println("PRODUCT PRICE:\t\tR " + found.getProductPrice());
            System.out.println("PRODUCT STOCK LEVELS:\t" + found.getStockLevel());
            System.out.println("PRODUCT SUPPLIER:\t" + found.getProductSupplier());
        } else {
            System.out.println("The product cannot be located. Invalid Product");
        }
        System.out.println("*******************************************************************");
    }

    public void UpdateProduct() {
        System.out.print("\nPlease enter the product code to update: ");
        String code = scanner.nextLine();
        ReportData found = findProductByCode(code);

        if (found == null) {
            System.out.println("The product cannot be located.");
            return;
        }

        System.out.print("Update the warranty? (y) Yes, (n) No: ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            System.out.print("Enter (1) for 6 months or any other key for 2 years: ");
            String wInput = scanner.nextLine();
            found.setProductWarranty(wInput.equals("1") ? "6 months" : "2 years");
        }

        System.out.print("Update the product price? (y) Yes, (n) No: ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            System.out.print("Enter the new price for " + found.getProductName() + " >> ");
            try {
                found.setProductPrice(Double.parseDouble(scanner.nextLine()));
            } catch (NumberFormatException e) {
                System.out.println("Invalid numeric input. Skipping price modification.");
            }
        }

        System.out.print("Update the stock level? (y) Yes, (n) No: ");
        if (scanner.nextLine().equalsIgnoreCase("y")) {
            System.out.print("Update the stock level? (y) Yes, (n) No >> ");
            try {
                found.setStockLevel(Integer.parseInt(scanner.nextLine()));
            } catch (NumberFormatException e) {
                System.out.println("Invalid entry. Skipping stock modification.");
            }
        }

        System.out.println("Product details have been updated successfully!!!");
    }
