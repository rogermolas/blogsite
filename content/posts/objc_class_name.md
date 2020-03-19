---
title: "Access class name using @objc attribute"
date: 2020-03-19T17:21:30+08:00
draft: faslse
categories: [Swift, Objective C,UITableView, UITableViewCell]
tags: [iOS, Swift, Objective C, UITableView, UITableViewCell]
author: rogermolas
---


**Scenario**
* Create Simple Table View app
* Load customs cells each row
* Cell identifier is class name, if object is TableCell cell identifier is "TableCell"
* Use common cell loading techniques
* Use helpher method to load cell using @objc attribute

**Create UITableViewCell subclass**
```
class HeaderCell: UITableViewCell {
    ...
}
```

```
class ContentsCell: UITableViewCell {
    ...
}
```

```
class AboutCell: UITableViewCell {
    ...
}
```

**Load cell in Tableview in traditional way**
```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    if indexPath.row == 0 {
        let cell = tableView.dequeueReusableCell(withIdentifier: "HeaderCell", for: indexPath) as? HeaderCell
        return cell
    }
    if indexPath.row == 2 {
        let cell = tableView.dequeueReusableCell(withIdentifier: "ContentsCell", for: indexPath) as? ContentsCell
        return cell
    }
    if indexPath.row == 1 {
        let cell = tableView.dequeueReusableCell(withIdentifier: "AboutCell", for: indexPath) as? AboutCell
        return cell
    }
    return UITableViewCell()
}
```

So whats **@objc** attribute?
When you apply it to a class or method it instructs Swift to make those things available to Objective-C as well as Swift code.

Most of time you see `@objc` when you call a method from a UIBarButtonItem or UIButton, you’ll need to mark that method using `@objc` so it’s exposed – both of those, and many others, are Objective-C code.

In this case we will use `@objc` to name our subclasses `HeaderCell`, `ContentsCell`, and `AboutCell` in Swift

**Update our UITableViewCell subclass**
```
@objc(HeaderCell)
class HeaderCell: UITableViewCell {
    ...
}
```
```
@objc(ContentsCell)
class ContentsCell: UITableViewCell {
    ...
}
```
```
@objc(AboutCell)
class AboutCell: UITableViewCell {
    ...
}
```

Create Helpher method to take cell intentifier using AnyClass type from UITableViewCell subclass.

**Note:Cell intentifier should be the class name**

```
func getCell(_ cls: AnyClass, _ index: IndexPath) -> AnyObject {
    let identifier = NSStringFromClass(cls)
    let cell = tableView.dequeueReusableCell(withIdentifier: identifier, for: index)
    return cell
}
```

**Load cell in Tableview using new way**
```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    if indexPath.row == 0 {
        let cell = getCell(HeaderCell.self, indexPath) as! HeaderCell
        return cell
    }
    if indexPath.row == 2 {
        let cell = getCell(ContentsCell.self, indexPath) as! ContentsCell
        return cell
    }
    if indexPath.row == 1 {
        let cell = getCell(AboutCell.self, indexPath) as! AboutCell
        return cell
    }
    return UITableViewCell()
}
```
Looks clean right?, so `@objc` attribute is not just for methods, we use it to name our class as well.

**Addition Tricks**

Lets make it more shorter, create enum of rows called `Row`

```
enum Row:Int {
    case HeaderCell = 0
    case ContentsCell = 1
    case AboutCell  = 2
    
    var className: AnyClass {
        switch self {
            case .Header:
                return HeaderCell.self
            case .Contents:
                return ContentsCell.self
            case .About:
                return AboutCell.self
        }
    }
}
```
```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let row = Row(rawValue: indexPath.row)
    let cell = getCell(row.className, indexPath) // dynamic biding
    return cell
}
```

That's it!
Thanks for your time