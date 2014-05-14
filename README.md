package oglesby;


import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.util.Date;

class BoughtPainting extends Painting implements  Comparable <BoughtPainting>
{

protected double suggestedMaximumPurchasePrice;
protected Date dateOfPurchase;
protected String nameOfSeller;
protected String addressOfSeller;
protected double actualPurchasePrice;
protected final double TARGET_PROFIT=2.15;
protected double targetSellingPrice;

    //Desc: constructor for BoughtPainting
    //Post: allow class to set the value of all Bought Painting fields in a record
    BoughtPainting(String fname, String lname, String work, Date dwork,
    String clas, double h, double w, String med, String sub, double max,
    Date d, String n, String a, double p)
    {
            artistFirstName=fname;
            artistLastName=lname;
            titleOfWork=work;
            dateOfWork=dwork;
            classification=clas;
            height=h;
            width=w;
            medium=med;
            subject=sub;
            suggestedMaximumPurchasePrice=max;
            dateOfPurchase=d;
            nameOfSeller=n;
            addressOfSeller=a;
            actualPurchasePrice=p;
            targetSellingPrice=actualPurchasePrice*TARGET_PROFIT;
    }
    //Desc: constructor for BoughtPainting
    //Post: instentiates a blank BoughtPainting object
    BoughtPainting()
    {
        artistFirstName="";
        artistLastName="";
        titleOfWork="";
        dateOfWork=new Date();
        classification="other";
        height=0;
        width=0;
        medium="other";
        subject="other";
        suggestedMaximumPurchasePrice=0;
        dateOfPurchase=new Date();
        nameOfSeller="";
        addressOfSeller="";
        actualPurchasePrice=0;
        targetSellingPrice=actualPurchasePrice*TARGET_PROFIT;
        dateOfPurchase= new Date();
    }

    //Desc: allows class to access the suggestedMaximumPurchasePrice field in a record
    //Return: suggestedMaximumPurchasePrice
    public double getSuggestedMaximumPurchasePrice()
    {
            return suggestedMaximumPurchasePrice;
    }

    //Desc:allows class to set the value of the suggestedMaximumPurchasePrice field in a record
    //Post: suggestedMaximumPurchasePrice is set to d
    public void setSuggestedMaximumPurchasePrice(double d)
    {
            suggestedMaximumPurchasePrice=d;
    }


    //Desc: allows class to access the dateOfPurchase field in a record
    //Return: dateOfPurchase
    public Date getDateOfPurchase()
    {
            return dateOfPurchase;
    }

    //Desc:allows class to set the value of the dateOfPurchase field in a record
    //Post: dateOfPurchase is set to d
    public void setDateOfPurchase(Date d)
    {
            dateOfPurchase=d;
    }

    //Desc: allows class to access the nameOfSeller field in a record
    //Return: nameOfSeller
    public String getNameOfSeller()
    {
            return nameOfSeller;
    }

    //Desc: allows class to set the value of the nameOfSeller field in a record
    //Post: nameOfSeller is set to n
    public void setNameOfSeller(String n)
    {
            nameOfSeller=n;
    }

    //Desc: allows class to access the addressOfSeller field in a record
    //Return: addressOfSeller
    public String getAddressOfSeller()
    {
            return addressOfSeller;
    }

    //Desc:allows class to set the value of the addressOfSeller field in a record
    //Post: addressOfSeller is set to a
    public void setAddressOfSeller(String a)
    {
            addressOfSeller=a;
    }

    //Desc: allows class to access the actualPurchasePrice field in a record
    //Return: actualPurchasePrice
    public double getActualPurchasePrice()
    {
            return actualPurchasePrice;
    }
    //Desc: allows class to set the value of the actualPurchasePrice
//      field in a record
    //Post: actualPurchasePrice is set to p
    public void setActualPurchasePrice(Double p)
    {
            actualPurchasePrice=p;
    }

    //Desc: allows class to access the targetSellingPrice field in a record
    //Return: targetSellingPrice
    public double getTargetSellingPrice()
    {
            return targetSellingPrice;
    }

    //Desc: allows class to set the value of the targetSellingPrice field
    //      in a record
    //Post: targetSellingPrice is set to t
    public void setTargetSellingPrice(Double t)
    {
            targetSellingPrice=t;
    }

    //Desc: updates the suggestedMaximumPurchasePrice in a record from user's input
    //Post: suggestedMaximumPurchasePrice field is updated
    public void updateSuggestedMaximumPurchasePrice()
    {
        try
        {
            System.out.println("Old Max Purchase Price:" + suggestedMaximumPurchasePrice);
            System.out.println("Please enter new Max Purchase Price and press <ENTER>: ");
            double tempmax=new Double(UserInterface.getString());
            suggestedMaximumPurchasePrice=tempmax;
        }

        catch (NumberFormatException e)
        {
           System.out.println("Value entered is not an double value. Please enter a double value: ");
           suggestedMaximumPurchasePrice=Double.parseDouble(UserInterface.getString());
           return;
        }
    }

    //Desc: updates the dateOfPurchase in a record from user's input
    //Post: dateOfPurchase field is updated
    public void updateDateOfPurchase()
    {
        try
        {
            System.out.println("Old Date of Purchase:" + dateOfPurchase);
            System.out.println("Please enter new Date of Purchase (mm/dd/yyyy) and press <ENTER>: ");
            Date tempDate=new Date(UserInterface.getString());
            dateOfPurchase=tempDate;
        }

        catch (NumberFormatException e)
        {
           System.out.println("Value entered is not a date value. Please enter a date value (mm/dd/yyyy): ");
           Date tempDate=new Date (UserInterface.getString());
           dateOfPurchase=tempDate;
           return;
        }
    }

    //Desc: updates the nameOfSeller in a record from user's input
    //Post: nameOfSeller field is updated
    public void updateNameOfSeller()
    {
        System.out.println("Old Name of Seller:" + nameOfSeller);
        System.out.println("Please enter new Name of Seller and press <ENTER>: ");
        nameOfSeller=UserInterface.getString();
    }

    //Desc: updates the addressOfSeller in a record from user's input
    //Post: addressOfSeller field is updated
    public void updateAddressOfSeller()
    {
        System.out.println("Old Address of Seller:" + addressOfSeller);
        System.out.println("Please enter new Address of Seller and press <ENTER>: ");
        addressOfSeller=UserInterface.getString();
    }

    //Desc: updates the actualPurchasePrice in a record from user's input
    //Post: actualPurchasePrice field is updated
    public void updateActualPurchasePrice ()
    {
        try
        {
            System.out.println("Old Actual Purchase Price:" + actualPurchasePrice);
            System.out.println("Please enter new Actual Purchase Price and press <ENTER>: ");
            double tempprice=new Double(UserInterface.getString());
            actualPurchasePrice=tempprice;
            targetSellingPrice=actualPurchasePrice*TARGET_PROFIT;
        }

        catch (NumberFormatException e)
        {
           System.out.println("Value entered is not an double value. Please enter a double value: ");
           actualPurchasePrice=Double.parseDouble(UserInterface.getString());
           targetSellingPrice=actualPurchasePrice*TARGET_PROFIT;
           return;
        }
    }

    //Desc: updates the targetSellingPrice in a record from user's input
    //Post: targetSellingPrice field is updated
    public void updateTargetSellingPrice()
    {
        try
        {
            System.out.println("Old Target Selling Price:" + targetSellingPrice);
            System.out.println("Please enter new Target Selling Price and press <ENTER>: ");
            double tempprice=new Double(UserInterface.getString());
            targetSellingPrice=tempprice;
        }

        catch (NumberFormatException e)
        {
           System.out.println("Value entered is not an double value. Please enter a double value: ");
           targetSellingPrice=Double.parseDouble(UserInterface.getString());
           return;
        }

    }

    //Desc:uses the last name of an artist and title of work to find a record in the file
    //Return: returns true if record is found or false if record is not found
    public boolean find(String alastname, String title)
    {
        try
        {
            File paintingsFile = new File ("GalleryPaintings.dat");
            boolean found = false;
            if (paintingsFile.exists())
            {
                RandomAccessFile inFile = new RandomAccessFile (paintingsFile, "r");
                while (!found && (inFile.getFilePointer()!=inFile.length()))
                {
                    read (inFile);
                    if (artistLastName.equalsIgnoreCase(alastname) &&
                    titleOfWork.equalsIgnoreCase(title))
                        found = true;
                }
                inFile.close();
            }
            return found;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: BoughtPainting.find () *****");
            System.out.println ("\t" + e);
            return false;
        }
    }

    //Desc: reads a single BoughtPainting record into an object from the fileName
    //Pre: RandomAccessFile must exist
    //Post: all Bought Painting fields from are read into this object
    public void read(RandomAccessFile fileName)
    {
        try
        {

            String  inputString = new String ();
            int	i = 0;
            inputString = fileName.readLine ();
            //Artist First Name
            StringBuffer input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistFirstName = input.toString ();
            i++;
            //Artist Last Name
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistLastName = input.toString ();
            i++;
            //Title of Work
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
             titleOfWork = input.toString ();
            i++;
            //Date of Work
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Date tempdow = new Date (input.toString ());
            dateOfWork = tempdow;
            i++;
           //classification
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            classification = input.toString ();
            i++; 
            //Height
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempheight = new Double (input.toString ());
            height = tempheight;
            i++;
            //Width
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempwidth = new Double (input.toString ());
            width = tempwidth;
            i++;
            //Medium
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            medium = input.toString();
            i++;
            //Subject
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            subject = input.toString();
            i++;
            //Suggested Max Purch Price
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempmax = new Double (input.toString ());
            suggestedMaximumPurchasePrice= tempmax;
            i++;

            //Date of Purchase
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Date tempdop = new Date (input.toString ());
            dateOfPurchase = tempdop;
            i++;
            //Name of Seller
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            nameOfSeller = input.toString();
            i++;
            //Address of Seller
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            addressOfSeller = input.toString();
            i++;
            //Actual Purchase Price
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempactual = new Double (input.toString());
            actualPurchasePrice = tempactual;
            i++;
            //Target Selling Price
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double temptarget = new Double (input.toString ());
            targetSellingPrice = temptarget;
            i++;
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: BoughtPainting.readsss () *****");
            System.out.println ("\t" + e);
        }

    }

    //Desc: writes all BoughtPainting fields to a record line in the specified file
    //Post: updates the specified file
    public void write(RandomAccessFile fileName)
    {
        try
        {
            fileName.writeBytes(artistFirstName + "|");
            fileName.writeBytes(artistLastName + "|");
            fileName.writeBytes(titleOfWork + "|");
            fileName.writeBytes(dateOfWork + "|");
            fileName.writeBytes(classification + "|");
            fileName.writeBytes(height + "|");
            fileName.writeBytes(width + "|");
            fileName.writeBytes(medium + "|");
            fileName.writeBytes(subject + "|");
            fileName.writeBytes(suggestedMaximumPurchasePrice + "|");
            fileName.writeBytes(dateOfPurchase + "|");
            fileName.writeBytes(nameOfSeller + "|");
            fileName.writeBytes(addressOfSeller + "|");
            fileName.writeBytes(actualPurchasePrice + "|");
            fileName.writeBytes(targetSellingPrice + "|"+ "\n");
        }
        catch (IOException e)
        {
            System.out.println ("***** Error: BoughtPainting.write () *****");
            System.out.println ("\t" + e);
        }
    }

    //Desc: saves an individual bought painting record into a file.  Will save over an
    //      existing record if the last name and title of work match or will add
    //      a new record if no existing record matches this object.
    //Pre:  all Bought Painting fields must be valid
    //Post: the message informing the user has been printed and the artist.dat
    //      file will be modified.
    public void save()
    {
        try
        {
            File paintingsFile = new File ("GalleryPaintings.dat");
            File  tempPaintingsFile = new File ("GalleryPaintings.tmp");
            BoughtPainting tempPainting = new BoughtPainting ();
            boolean found = false;
            RandomAccessFile newFile = new RandomAccessFile (tempPaintingsFile, "rw");
            if (!paintingsFile.exists ())
            {
              write(newFile);
            }
            else
            {
                RandomAccessFile oldFile = new RandomAccessFile (paintingsFile, "r");
                boolean comparePaintings;
                while (oldFile.getFilePointer () != oldFile.length ())
                {
                    tempPainting.read(oldFile);
                    if (artistLastName.equalsIgnoreCase(tempPainting.getArtistLastName()) &&
                    titleOfWork.equalsIgnoreCase(tempPainting.getTitleofWork()))
                        comparePaintings=true;
                    else comparePaintings=false;
                    if(comparePaintings)
                    {
                        write (newFile);
                        found=true;
                    }
                    else
                    {
                      tempPainting.write(newFile);
                    }
                }
                if (!found) write (newFile);
                oldFile.close ();
            }
            newFile.close ();
            paintingsFile.delete ();
            tempPaintingsFile.renameTo (paintingsFile);
            System.out.println("record saved to file");
        }
        catch (Exception e)
        {
            System.out.println ("***** Error: BoughtPainting.putRecord () *****");
            System.out.println ("\t" + e);
        }
    }

    //Desc: reads in all fields into a Painting object from user input
    //Post: artistFirstName, artistLastName, and fashionabilityValue are modified
    public void readInRecord()
    {
        try
        {
            System.out.println("Enter Artist First name: ");
            artistFirstName = UserInterface.getString();

            System.out.println("Enter Artist Last name: ");
            artistLastName= UserInterface.getString();

            System.out.println("Enter title of painting: ");
            titleOfWork = UserInterface.getString();

/*            System.out.println("Enter classification of Painting (masterpiece, masterwork, or other): ");
            classification = UserInterface.getString();
            while (!(classification.equalsIgnoreCase("masterpiece")|classification.equalsIgnoreCase("masterwork")|
                    classification.equalsIgnoreCase("other")))
            {
                System.out.println("Classification entered incorrectly. Please enter one of the following mediums: masterpiece, masterwork, or other.");
                classification=UserInterface.getString();
            }
*/
            System.out.println("Enter the date the painting was created (mm/dd/yyyy): ");
            Date tempdate = new Date(UserInterface.getString());
            dateOfWork=tempdate;

            System.out.println("Enter painting medium (oil, watercolor, or other): ");
            medium  = UserInterface.getString();
            while (!(medium.equalsIgnoreCase("oil")|medium.equalsIgnoreCase("watercolor")|
                    medium.equalsIgnoreCase("other")))
            {
                System.out.println("Medium entered incorrectly. Please enter one of the following mediums: oil, watercolor, or other.");
                medium=UserInterface.getString();
            }

            System.out.println("Enter painting subject (portrait, still-life, landscape, or other): ");
            subject =UserInterface.getString();
            while (!(subject.equalsIgnoreCase("portrait")|subject.equalsIgnoreCase("still-life")|
            subject.equalsIgnoreCase("landscape")| subject.equalsIgnoreCase("other")))
            {
                System.out.println("Subject entered incorrectly. Please enter one of the following subjects: portrait, still-life, landscape, or other.");
                subject=UserInterface.getString();
            }

            System.out.println("Enter painting width: ");
            Double tempw=new Double( UserInterface.getString());
            width =tempw;

            System.out.println("Enter painting height: ");
            Double temph=new Double(UserInterface.getString());
            height =temph;
        }

        catch (Exception e)
        {
           System.out.println("Record value entered is not the correct data type. Please re-enter the record: ");
           readInRecord();
        }

    }

    //Desc: Deletes a single record in the GalleryPaintings.dat File if the artist last
    //      name and first name matches this object.
    //Post: Modifies the GalleryPaintings.dat File
    public void performDeletion ()
    {
        try
        {
            File  paintingsFile = new File ("GalleryPaintings.dat");
            File  tempPaintingsFile = new File ("GalleryPaintings.tmp");

            BoughtPainting bp = new BoughtPainting ();	// record to be checked

            if (!paintingsFile.exists ())
            {
              return;
            }

            RandomAccessFile inFile = new RandomAccessFile (paintingsFile, "r");
            RandomAccessFile outFile = new RandomAccessFile (tempPaintingsFile, "rw");

            while (inFile.getFilePointer () != inFile.length ())
            {
              bp.read (inFile);

              if (!(artistLastName.equalsIgnoreCase(bp.getArtistLastName()) &&
                        titleOfWork.equalsIgnoreCase(bp.getTitleofWork())))
              {
                  bp.write (outFile);
              }
            }

            inFile.close ();
            outFile.close ();

            paintingsFile.delete ();
            tempPaintingsFile.renameTo (paintingsFile);

        }
        catch (Exception e)
        {
            System.out.println ("***** Error: BoughtPainting.performDeletion () *****");
            System.out.println ("\t" + e);
        }
    }

    public void print ()
    {
      System.out.print ("Artist First Name: " + artistFirstName);
      System.out.print ("\t Artist Last Name: " + artistLastName);
      System.out.print ("\t Title Of Work: " + titleOfWork);
      System.out.print ("\t Date Of Work: " + dateOfWork);
      System.out.print ("\t Classification: " + classification);
      System.out.print ("\t Height: " + height);
      System.out.print ("\t Width: " + width);
      System.out.print ("\t Medium: " + medium);
      System.out.print ("\t Subject: " + subject);
      System.out.print ("\t Suggested Max Purchase Price: " + suggestedMaximumPurchasePrice);
      System.out.print ("\t Date Of Purchase: " + dateOfPurchase);
      System.out.print ("\t Name Of Seller: " + nameOfSeller);
      System.out.print ("\t Address Of Seller: " + addressOfSeller);
      System.out.print ("\t Actual Purchase Price: " + actualPurchasePrice);
      System.out.println ("\t Target Selling Price: " + targetSellingPrice);
    }


  //Desc: prompts the user to enter the special bought painting fields so that
  //    the painting the user buys can be added to "GalleryPainting.dat"
  //Pre: all of the values from painting class must already be set
  //Post: GalleryPainting.dat will have the new painting added to the records
  public void addRecentlyBought ()

  {
    try
    {



        System.out.println("Enter the date the painting was purchased (mm/dd/yyyy): ");
        Date tempdate = new Date(UserInterface.getString());
        dateOfPurchase=tempdate;

        System.out.println("Enter Seller's name: ");
        nameOfSeller = UserInterface.getString();

        System.out.println("Enter Seller's address: ");
        addressOfSeller = UserInterface.getString();

        System.out.println("Enter painting actual purchase price: ");
        Double tempw=new Double( UserInterface.getString());
        actualPurchasePrice =tempw;


        targetSellingPrice=actualPurchasePrice*TARGET_PROFIT;

	save ();
	System.out.println ("\nThe following record was inserted\n");
	print ();


    }
    catch (Exception e)
    {
	System.out.println ("***** Error: BoughtPainting.addRecentlyBought () *****");
	System.out.println ("\t" + e);
    }

  }  
     @Override
    public int compareTo(BoughtPainting comparePainting) 
    {
        return classification.compareToIgnoreCase(comparePainting.getClassification());
    } 
}
