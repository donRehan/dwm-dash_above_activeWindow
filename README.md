dash_above_activeWindow
=============

Description
-----------
Create a line above active window with schemeSel color , while setting
the background of text to the schemeNorm

![screenshot of the activewindow in the bar after patch](preview.png)

Config variables are avaliable to edit the width of bar dash , its y-position
as well as text y-position in the bar.

> [!NOTE]
> If you are using [bidi patch](https://dwm.suckless.org/patches/bidi/)
> Make sure to move apply_fribidi just above drw_text.

> [!NOTE]
> if you are using [awesome bar](https://dwm.suckless.org/patches/awesomebar/)
> Use the below example to make sure its working with you for the active window.

```bash

@@ -940,12 +940,7 @@ drawbar(Monitor *m)
                        for (c = m->clients; c; c = c->next) {
                                if (!ISVISIBLE(c))
                                        continue;
-                               if (m->sel == c)
-                                       scm = SchemeNorm;
-                               else if (HIDDEN(c))
-                                       scm = SchemeHid;
-                               else
-                                       scm = NonCurrWin;
+        scm = SchemeNorm;
                                drw_setscheme(drw, scheme[scm]);
 
                                if (remainder >= 0) {
@@ -959,7 +954,15 @@ drawbar(Monitor *m)
                                //drw_rect(drw, x, -15, tabw , bh, 1, 1);
                                //drw_setscheme(drw, scheme[SchemeNorm]);
                                drw_text(drw, x, 0, tabw, bh, lrpad / 2, fribidi_text, 0);
-                               drw_rect(drw, x , bh - 18 , tabw , 2, 1, 0);
+        
+        //if the client is selected
+        if(m->sel == c) {
+          drw_setscheme(drw, scheme[SchemeSel]);
+          int dash_width = tabw;  // Width of the dash
+          int dash_height = 2;  // Height of the dash 
+          drw_rect(drw, x, 0, tabw, dash_height, 1, 1);  
+        }
+
                                x += tabw;
```

Download
--------
* [dwm-dash_above_activeWindow-20240604-061e9fe.diff](dwm-dash_above_activeWindow-20240604-061e9fe.diff)

Author
------
* [Alhussien Ahmed](https://github.com/donRehan)
