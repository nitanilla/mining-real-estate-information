jquery.modalize.js
========

[jquery.modalize.js](https://github.com/toddway/jquery.modalize) is a lightweight, pure-javascript approach to automatically turn part of any web page into a modal overlay.  

It was originally designed as a simple alternative for associating file upload fields to WYSIWYGs in Drupal, but can be used to modalize any chunk of HTML on any page (Drupal or non-Drupal) and significantly clean up overloaded pages. 

## The original dilemma
I've never loved any of the solutions for associating image and file uploads to WYSIWYGs in Drupal and yet I've had to do it on almost every project I've worked on.  The [Media module](http://drupal.org/project/media) and the [Wysiwyg Fields module](http://drupal.org/project/wysiwyg_fields) are both ambitious projects that attempt this feature (and other things as well).  Unfortunately I've run into issues with both.  Being complex modules they are difficult to troubleshoot and hard to move away from if they don't work out.

## My usual solution
I normally end up sticking a multi-value image field and a multi-value file field underneath the WYSIWYG and then using the excellent [Insert module](http://drupal.org/project/insert) to allow content editors to "send" HTML for the uploaded files to the WYSIWYG.  

<img src="https://dl.dropbox.com/u/862951/md/no-modal.png" style="border:1px solid #ccc;width:400px"/>

This is reliable and works nicely, but has a few drawbacks:

1. It takes up lot of screen real estate - especially if you upload many files
2. The WYSIWYG associations aren't immediately intuitive to users - sometimes they have to scroll to see the whole picture
3. If you have more than one WYSIWYG on a page it's even harder to infer the associations.

## The new modally-powered solution
With jquery.modalize.js, I start with my usual solution (as described above), add a single line of jQuery to turn my file fields into modals, and attach them to every WYSIWYG on the page. 

<img src="https://dl.dropbox.com/u/862951/md/modal-links.png" style="border:1px solid #ccc;width:400px"/>

<img src="https://dl.dropbox.com/u/862951/md/opened-modal.png" style="border:1px solid #ccc;width:400px"/>


To use it you just need JQuery, jquery.modalize.js, and a line of code like this:

    $.modalize('#edit-field-image-attachments', '+ Attach images', '.field-type-text-with-summary');
     
       
       
This turns the `#edit-field-image-attachments` element into a hidden modal, replaces it with a link labeled *+ Attach images* and prepends the link to all elements with the `.field-type-text-with-summary` class (covers WYSIWYG fields in Drupal).  Clicking on the link will open the modal as a page overlay.  The third argument is optional and if not provided, the modal link will be attached in the original element's DOM location. 

As a bonus, Modalize is Insert module aware, so clicking the Insert button will automatically close the modal and show the user the WYSIWYG it was inserted into.
