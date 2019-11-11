PNG console app
Development on hold, 09/2018
It contains code and standards for the insertion of CloudCoins into PNG.
Goal
To insert, save, and retrieve data from the PNG file format.
Summary of implementation
Add new png. It allows the user to target a PNG image from the "png" folder.
Select your png. It allows the user to target a PNG image from the "Image Bank" folder.
Select your CloudCoins. It allows a user to select one or multiple CloudCoin stacks found in the Bank folder.
Insert the CloudCoins into the PNG. Inserts the CloudCoins as a png chunk with the chunk type designator of cLDc.
CloudCoins to Printouts folder. Searches the file for cLDc chunk types, copies the information to the printouts folder. Creates a new image without the CloudCoin metadata.
Overview of implementation.
The current implementation is a console app built-in VS-Code, to be upgraded to a multi-platform application.
It serves as a proof of concept for storing CloudCoins in the meta tags of PNG files.


### Overview of implementation.

    The current implementation is a console app built in VS-Code, to be upgraded to a multi-platform application.
    it serves as a proof of concept for storing CloudCoins in the meta tags of PNG files.


#### Add new png

png = new PngClass();

Prompt the user for an image path.
use the path to build the PngClass.

```         //Program.cs
            string filepath = SelectNewPNG("./Images");

            //PngClass.cs
            setpath(filepath); //done
            updatePNG();
```
#### Select you png

Prompt the user to select an existing image from the ImageBank folder.
use the path to build the PngClass.

```         //Program.cs
            png = new PngClass(true);

            //PngClass.cs
            string filepath = SelectNewPNG("./ImageBank");
            setpath(filepath); //done
            updatePNG();
```

#### Select your CloudCoins.

Allows the user to stage CloudCoins in the ImageClass.
```         //Program.cs
            png.stageCoins();

            //PngClass.cs
            setHasStagedCoins();
            setStagedValue();
```

#### Insert the CloudCoins into the PNG 

Splits the png before the IEND chunk, appends the CloudCoins then the IEND chunk. 
```         //Program.cs
            if(png.hasStagedCoins)
                png.SaveCoins();
            png.updatePNG();

            //PngClass.cs
            setworkingname();
            updatePNG();
            write();
```
#### CloudCoins to Printouts folder. 

Saves any CloudCoins stored in an image folder to the Printouts folder.
Duplicates the image without the CloudCoin data.
```         //Program.cs
            png.removeCoins();

            //PngClass.cs
            updatePNG();
            write(coin.ccData, "./Printouts/"+coin.name);
```


#### PNG Standard
![Standard](./standards/PNG_Header_Standard.png)

[Header](./standards/PNG_Header_Standard.png)  |  [Body](./Standards/PNG_Body_Standard.png) 



