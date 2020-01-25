#Computing W Matrix

this source gets 10 image of cfar-10 and computing the result image  

#Exampel

##Inputs
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse1.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse2.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse3.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse4.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse5.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse6.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse7.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse8.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse9.png" width="32" height="32" />
<img src="https://www.cs.toronto.edu/~kriz/cifar-10-sample/horse10.png" width="32" height="32" />


##Output

<img src="http://uupload.ir/files/xmji_output.png" width="32" height="32" />


#Java Source

```java

    private void W(File folder) throws IOException {


        ArrayList<ListImageByte> list = new ArrayList<>();
        Main main = new Main();

        for (File image : folder.listFiles()) {

            if (!image.isDirectory()) {

                int[][][][][] rgb = main.RGB(image);
                ListImageByte aByte = new ListImageByte();
                aByte.setBytes(rgb);
                list.add(aByte);

            }

        }


        int[][][][][] rgb1 = list.get(0).getBytes();
        int[][][][][] rgb2 = list.get(1).getBytes();
        int[][][][][] rgb3 = list.get(2).getBytes();
        int[][][][][] rgb4 = list.get(3).getBytes();
        int[][][][][] rgb5 = list.get(4).getBytes();
        int[][][][][] rgb6 = list.get(5).getBytes();
        int[][][][][] rgb7 = list.get(6).getBytes();
        int[][][][][] rgb8 = list.get(7).getBytes();
        int[][][][][] rgb9 = list.get(8).getBytes();
        int[][][][][] rgb10 = list.get(9).getBytes();
        int[][][][][] rgbOut = new int[32][32][3][3][3];

        for (int i = 0; i < 32; i++) {

            for (int j = 0; j < 32; j++) {

                int r = 0, g = 0, b = 0;


                r = (rgb1[j][i][0][0][0] + rgb2[j][i][0][0][0] + rgb3[j][i][0][0][0] + rgb4[j][i][0][0][0] + rgb5[j][i][0][0][0] + rgb6[j][i][0][0][0] + rgb7[j][i][0][0][0] + rgb8[j][i][0][0][0] + rgb9[j][i][0][0][0] + rgb10[j][i][0][0][0]) / list.size();
                g = (rgb1[j][i][1][1][1] + rgb2[j][i][1][1][1] + rgb3[j][i][1][1][1] + rgb4[j][i][1][1][1] + rgb5[j][i][1][1][1] + rgb6[j][i][1][1][1] + rgb7[j][i][1][1][1] + rgb8[j][i][1][1][1] + rgb9[j][i][1][1][1] + rgb10[j][i][1][1][1]) / list.size();
                b = (rgb1[j][i][2][2][2] + rgb2[j][i][2][2][2] + rgb3[j][i][2][2][2] + rgb4[j][i][2][2][2] + rgb5[j][i][2][2][2] + rgb6[j][i][2][2][2] + rgb7[j][i][2][2][2] + rgb8[j][i][2][2][2] + rgb9[j][i][2][2][2] + rgb10[j][i][2][2][2]) / list.size();

                rgbOut[j][i][0][0][0] = r;
                rgbOut[j][i][1][1][1] = g;
                rgbOut[j][i][2][2][2] = b;

            }

        }


        BufferedImage out = ImageIO.read(new File("template.png"));


        for (int i = 0; i < 32; i++) {

            for (int j = 0; j < 32; j++) {

                int r = rgbOut[j][i][0][0][0];
                int g = rgbOut[j][i][1][1][1];
                int b = rgbOut[j][i][2][2][2];

                int p = (r << 16) | (g << 8) | b;
                out.setRGB(j, i, p);

            }

        }


        File f = new File("Output.png");
        ImageIO.write(out, "png", f);


    }


    private int[][][][][] RGB(File f) throws IOException {


        BufferedImage img = ImageIO.read(f);

        int[][][][][] bytes = new int[img.getHeight()][img.getWidth()][3][3][3];

        for (int i = 0; i < img.getWidth(); i++) {

            for (int j = 0; j < img.getHeight(); j++) {

                int p = img.getRGB(j, i);
                int r = (p >> 16) & 0xff;
                int g = (p >> 8) & 0xff;
                int b = p & 0xff;

                bytes[j][i][0][0][0] = r;
                bytes[j][i][1][1][1] = g;
                bytes[j][i][2][2][2] = b;

            }


        }


        return bytes;


```

