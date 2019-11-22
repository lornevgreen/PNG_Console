# PNG console app
## Development on hold, 09/2018
Contains code and standards for the insertion of CloudCoins into PNG.


## Goal

#### To insert, save and retreive data from the PNG file format.

## Summary of implementation

1) Add new png.
`Allows the user to target a PNG image from the "png" folder. `
2) Select your png.
`Allows the user to target a PNG image from the "Image Bank" folder. `
3) Select your CloudCoins.
`Allows a user to select one or multiple CloudCoin stacks found in the Bank folder.`
4) Insert the CloudCoins into the PNG.
`Inserts the CloudCoins as a png chunk with the chunk type designator of cLDc.`
5) CloudCoins to Printouts folder.
`Searches the file for cLDc chunk types, copies the information to the printouts folder.`
`Creates a new image without the CloudCoin meta data.`



### Overview of implementation.

    The current implementation is a console app built-in VS-Code, to be upgraded to a multi-platform application.
It serves as a proof of concept for storing CloudCoins in the meta tags of PNG file


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

Allows the user to stage CloudCoins in the Image class.
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



