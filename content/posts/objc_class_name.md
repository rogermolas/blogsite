---
title: "Access class Name using @objc attribute"
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

**Create UITableViewCell classes**
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