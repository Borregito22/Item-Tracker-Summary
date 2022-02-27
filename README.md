# Item-Tracker-Summary

## Introduction
For the last two weeks at The Tech Academy, I worked on building a Database collection manager using Python and the Django Framework. I worked with a team where everybody built individual apps that are accessible from the home page of the project. The app I built allows users to input an item to keep track of with certain details about the item. 

## CRUD Functionality
Overall, users are allowed to input an item, then have the option to update or delete the item from the database. The items are displayed on a table in alphabetical order.

### Create
I created a form that has all the inputs necessary to save an item to the database. The function takes the inputs and save it to the database.

```
def eft_create_record(request):
    form = EFTForm(request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('eft_create_record')
    else:
        print(form.errors)
        form = EFTForm()
    context = {
        'form': form,
    }
    return render(request, 'EFT_Items/EFT_Items_create.html', context)
```
![Input Form](https://github.com/[borregito22]/[Item-Tracker-Summary]/blob/[Screenshots]/160342.png?raw=true)

### Read


### Update and Delete
