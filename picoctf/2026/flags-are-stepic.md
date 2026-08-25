hello! 🍏 this ctf was one of the more interesting ones i've done so far;

<img width="352" height="344" alt="Screenshot 2026-08-25 at 18 26 32" src="https://github.com/user-attachments/assets/17ab14b3-519f-4715-b3e5-ab2bb550ed8e" />

the description of the ctf tells us that there's some sort of a secret message hidden within the website, upon opening it, you're greeted with tons of flags of countries.
the hint tells us that;
"In the country that doesn't exist, the flag persists" - so looking for the country that doesn't exist is the obvious choice. 
scrolling down you see Upanzi, the made up country, and if the name + flag isn't what gives it away, then it's the massive file size you can see in dev tools.

<img width="761" height="378" alt="image" src="https://github.com/user-attachments/assets/4a3f98f6-2c26-4559-92e9-a4c80f63ef93" />
<img width="749" height="449" alt="Screenshot 2026-08-25 at 18 30 32" src="https://github.com/user-attachments/assets/bedf54ac-d6ef-4197-b56a-43b6a6d2c987" />

next thing i did was download the image and run it through binwalk but i didn't have much luck. we're out of actual hints but name of the ctf itself is a hint:
stepic is a linux steganography library, steganography being the hiding of information inside something that doesn't look like it contains information, for example, an image!
i wasn't really familiar with the usage of stepic before this, but this [stackoverflow post](https://stackoverflow.com/questions/16838341/steganography-in-python-stepic) really helped.
i wrote a short python script for this - 
```from PIL import Image
import stepic

im1 = Image.open('upz.png')
s = stepic.decode(im1) 
print(s)
```

now, i initially tried to solve this in the webshell provided by picoctf, however when running it i got this

<img width="888" height="78" alt="image" src="https://github.com/user-attachments/assets/46d66541-4162-4bf7-a7b0-548009affcda" />

the file contains around 150 million pixels and the webshell simply ran out of memory and killed it.
so i switched to my own terminal and after installing pillow and stepic i ran it no problem, the only thing you should be mindful of is running the script in the same folder as the png.

<img width="570" height="86" alt="5B64DEEE-C908-4F4C-8305-3ABE1372B5B8_4_5005_c" src="https://github.com/user-attachments/assets/c715f18c-ea03-4634-91bb-c277ebf5a36f" />

i learned a lot from this ctf + stackoverflow really helped, as did just simply slowing down and reading the outputs i was getting. 


 
