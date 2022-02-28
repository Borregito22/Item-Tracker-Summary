# Item-Tracker-Summary

## Introduction
For the last two weeks at The Tech Academy, I worked on building a Database collection manager using Python and the Django Framework. I worked with a team where everybody built individual apps that are accessible from the home page of the project. The app I built allows users to input an item to keep track of with certain details about the item. I was particularly proud of the instant search bar to filter results from the database. My instructor sent me a link to DataTables which is a plug-in for the jQuery JavaScript library. URL: https://datatables.net/

## CRUD Functionality
Overall, users are allowed to input an item, then have the option to update or delete the item from the database. The items are displayed on a table in alphabetical order.

### Create
I created a form that has all the inputs necessary to save an item to the database. The function takes the inputs and save it to the database.

```
def eft_create_record(request):
    form = EFTForm(request.POST or None)
    if form.is_valid():
        form.save()
        return redirect('eft_all_items')
    else:
        print(form.errors)
        form = EFTForm()
    context = {
        'form': form,
    }
    return render(request, 'EFT_Items/EFT_Items_create.html', context)
```
![Input Form](https://github.com/Borregito22/Item-Tracker-Summary/blob/main/Screenshots/160342.png?raw=true)

### Read
I created a table to render the items saved in the database, and added an instant search bar to filter the items. Additionally, the user is able to click on a details link to display the details about the selected item.

```
def eft_all_items(request):
    # Gets all objects from the database sorted by name
    sorted_items = EFTItems.objects.order_by('name')
    return render(request, 'EFT_Items/EFT_Items_display_items.html', {'items': sorted_items})
```
```
def eft_details(request, pk):
    details = get_object_or_404(EFTItems, pk=pk)
    context = {
        'details': details,
    }
    return render(request, 'EFT_Items/EFT_Items_details.html', context)
```
![Table](https://github.com/Borregito22/Item-Tracker-Summary/blob/main/Screenshots/163743.png?raw=true)

### Update and Delete
The user can edit and delete objects from the database from the details page of the selected item. There's a popup window to confirm the user would like to delete the object. The delete function is pretty simple and functions as necessary.

```
$(document).on('click', '.confirm_delete', function(){
                return confirm('Are you sure you want to delete this item?');
            })
```
```
def eft_edit(request, pk):
    items = EFTItems.objects.get(pk=pk)
    form = EFTForm(request.POST or None, instance=items)
    if form.is_valid():
        form.save()
        return redirect('eft_all_items')
    context = {
        'items': items, 'form': form
    }
    return render(request, 'EFT_Items/EFT_Items_edit.html', context)
```
```
def eft_delete(request, pk):
    item = EFTItems.objects.get(pk=pk)
    item.delete()
    return redirect('eft_all_items')
```
![Confirm Delete](https://github.com/Borregito22/Item-Tracker-Summary/blob/main/Screenshots/170108.png?raw=true)

## Skills Acquired
* Utilizing Version Control to keep everyone's code clean and to prevent the master branch from accidentally breaking
* Learned to debug/create code from finding similar examples from other developers and seeing how they got their code to function