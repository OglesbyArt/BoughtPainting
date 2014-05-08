package artpricingsystem;

import java.io.File;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.util.Date;
import java.util.Scanner;

class BoughtPainting extends Painting 
{

protected Date dateOfPurchase;
protected String nameOfSeller;
protected String addressOfSeller;
protected double actualPurchasePrice;
protected double targetSellingPrice;

    //Desc: constructor for BoughtPainting
    //Post: allow class to set the value of all Bought Painting fields in a record
    BoughtPainting(String fname, String lname, String work, Date dwork, 
    String clas, double h, double w, String med, String sub, double max, 
    Date d, String n, String a, double p, double t)
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
            targetSellingPrice=t;
    }
    //Desc: constructor for BoughtPainting
    //Post: allows class to set a new record for a Bought Painting
    BoughtPainting()
    {
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

    //Desc: Finds the record the user wants to update and updates the 
    //		dateOfPurchase field in the found object
    //Post: dateOfPurchase field is updated
    public void updateDateOfPurchase() //will this ever change?
    {
        System.out.println("Old Date of Purchase:" + dateOfPurchase);
        System.out.println("Please enter new Date of Purchase and press <ENTER>: \n");
        Date tempDate=new Date(UserInterface.getString());
        dateOfPurchase=tempDate;
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		nameOfSeller field in the found object
    //Post: nameOfSeller field is updated
    public void updateNameOfSeller()
    {
        System.out.println("Old Name of Seller:" + nameOfSeller);
        System.out.println("Please enter new Name of Seller and press <ENTER>: \n");
        nameOfSeller=UserInterface.getString();
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		addressOfSeller field in the found object
    //Post: AddressOfSeller field is updated
    public void updateAddressOfSeller()
    {
        System.out.println("Old Address of Seller:" + addressOfSeller);
        System.out.println("Please enter new Address of Seller and press <ENTER>: \n");
        addressOfSeller=UserInterface.getString();
    }

    //Desc: Finds the record the user wants to update and updates the 
    //		actualPurchasePrice field in the found object
    //Post: actualPurchasePrice field is updated
    public void updateActualPurchasePrice ()
    {
        System.out.println("Old Actual Purchase Price:" + actualPurchasePrice);
        System.out.println("Please enter new Actual Purchase Price and press <ENTER>: \n");
        double tempprice=new Double(UserInterface.getString());
        actualPurchasePrice=tempprice;
    }
	
	//Desc: Finds the record the user wants to update and updates the 
	//		targetSellingPrice field in the found object
	//Post: targetSellingPrice field is updated
	public void updateTargetSellingPrice() //will this ever change?
	{
            System.out.println("Old Target Selling Price:" + targetSellingPrice);
            System.out.println("Please enter new Target Selling Price and press <ENTER>: \n");
            double tempprice=new Double(UserInterface.getString());
            targetSellingPrice=tempprice;
	}
	
    //Desc: uses the last name of an artist and the title of work to find the
    // 		 Bought Painting object in the array 
    //Return: returns the found Artist object or null value if Artist not found
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

	//Desc: reads a file into the scanner, sets each field in the text file to 
	//		a field in a new Bought Painting object
	//Pre: file must exist
	public void read(RandomAccessFile fileName)
    {
        try
        {
            String  inputString = new String ();	// for storing artist record
            int	i = 0;		                // position in record
            inputString = fileName.readLine ();
            StringBuffer input = new StringBuffer ();	// for storing field within record
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistFirstName = input.toString ();
            i++;

            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            artistLastName = input.toString ();
            i++;

            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
             titleOfWork = input.toString ();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++; 
            }
             Date tempdow = new Date (input.toString ());
             dateOfWork = tempdow;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
             classification = input.toString ();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempheight = new Double (input.toString ());
            height = tempheight;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempwidth = new Double (input.toString ());
            height = tempwidth;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            medium = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            subject = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempmax = new Double (input.toString ());
            suggestedMaximumPurchasePrice= tempmax;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Date tempdop = new Date (input.toString ());
            dateOfPurchase = tempdop;
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            nameOfSeller = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            addressOfSeller = input.toString();
            i++;
            
            input = new StringBuffer ();
            while (inputString.charAt (i) != '|')
            {
              input.append (inputString.charAt (i));
              i++;
            }
            Double tempactual = new Double (input.toString ());
            actualPurchasePrice = tempactual;
            i++;
            
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
            System.out.println ("***** Error: BoughtPainting.read () *****");
            System.out.println ("\t" + e);
        }

      }
	//Desc: writes the variables dateOfPurchase, nameOfSeller, addressOfSeller, 
	//		actualPurchasePrice, and targetSellingPrice to a record in the file
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
                //double check that this writes doubles, ints, and dates correctly
            }
            catch (IOException e)
            {
                System.out.println ("***** Error: BoughtPainting.write () *****");
                System.out.println ("\t" + e);
            }
        }
    //Desc: writes the record back to the text file and prompts the 
    //      user the data has been saved
    //Post: changes the text file
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
    
    public void performDeletion()
    {
               System.out.println("performdeletion");
    try
    {
	File  galleryPainting = new File ("GalleryPaintings.dat");
	File  tempgalleryPainting = new File ("painting.tmp");

	BoughtPainting bp = new BoughtPainting();	// record to be checked

	if (!galleryPainting.exists ())
	{
            System.out.println("galleryPainting doesn't exist");
	  return;
	}

	RandomAccessFile inFile = new RandomAccessFile (galleryPainting, "r");
	RandomAccessFile outFile = new RandomAccessFile (tempgalleryPainting, "rw");

	while (inFile.getFilePointer () != inFile.length ())
	{
	  bp.read (inFile);
          System.out.println("Read");

          if ((artistLastName.compareTo (bp.getArtistLastName ()) != 0) && (
                  titleOfWork.compareTo(bp.getTitleofWork()) !=0))
	  {
              System.out.println("write");
	      bp.write (outFile);
	  }
	}
         System.out.println("before close");
	inFile.close ();
	outFile.close ();
         System.out.println("after close");

	galleryPainting.delete ();
        System.out.println("deleted");
	tempgalleryPainting.renameTo (galleryPainting);

    }
    catch (Exception e)
    {
	System.out.println ("***** Error: Investment.performDeletion () *****");
	System.out.println ("\t" + e);
    }
    }
    
    public void readInRecord()
    {
        //grab this from the UI class!
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

    //  obtains input data for all fields of a Painting record.
    public void readInRecord()
    {
        try
        {
            char c;				// character entered by user
            String input;                      	// buffer for line of characters
            boolean valid = false;      		// used to validate length of ID
            System.out.println("Enter Artist First name: ");
            artistFirstName = UserInterface.getString();
            System.out.println("Enter Artist Last name: ");
            artistLastName= UserInterface.getString();
            System.out.println("Enter title of painting: ");
            titleOfWork = UserInterface.getString();
            System.out.println("Enter the date the painting was created (mm/dd/yyyy): ");
            Date tempdate = new Date(UserInterface.getString());
            //catch errors on date not converting here
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
            width =tempw; //error check if it can't be converted to a double
            System.out.println("Enter painting height: ");
            Double temph=new Double( UserInterface.getString());
            height =temph;//error check if it can't be convereted to a double
        }
          catch (Exception e)
          {
            System.out.println ("***** Error: Investment.readInvestmentData () *****");
            System.out.println ("\t" + e);
          }
    }
}
