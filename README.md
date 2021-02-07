# efig

## Requires

- pdfimages

- python

## Show
![efig](./screenshot/efig.gif)

## Install
```shell
git clone https://github.com/demonlord1997/efig
```
(If you only use it in [ranger](https://github.com/ranger/ranger), you don't need to install it.)
## Usage

### Use In Shell
you can customize the command named `efig` in your `.bashrc` or `.zshrc`.
```shell
alias efig='python <path of efig.py>'
```

Then, you can use `efig` to extract images from a pdf.
```shell
efig -i <PDF-file>
```

### Use In Ranger

If you want to use efig in ranger, you don't need to clone the repository. I have prepared the class named `efig` for you:
```python
class efig(Command):
    """
    :efig <fname>

    extract all image from pdf.

    Will create a folder named "images" in the current folder.

    """
    def execute(self):
        from subprocess import call

        if not os.path.exists("images"):
            os.makedirs("images")

        if not self.arg(1):
            input_file = self.fm.thisfile.path
        else:
            input_file = self.rest(1)

        output = input_file[0:-4]
        call(['pdfimages', '-png', input_file, 'images/'+output])

    def tab(self, tabnum):
        return self._tab_directory_content()
```
You can copy the class into `commands.py` of ranger. (~/.config/ranger/commands.py)

Then you can input `:efig <PDF-file>` in ranger.

![efig](./screenshot/efig.gif)
