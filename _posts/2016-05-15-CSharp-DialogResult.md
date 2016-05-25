---
layout: post
title:  "CSharp DialogResult"
date:   2016-05-15
excerpt: "Programımız çalışmaya başlarken kullanıcı girişini sağlamak amacı ile DialogResult yapıyoruz"
tag:
- CSharp 
- DialogResult
- User Password
comments: false
---

[DialogResult MSDN Microsoft](https://msdn.microsoft.com/tr-tr/library/system.windows.forms.dialogresult(v=vs.110).aspx)


## Kullanımı

### Method

{% highlight c# %}
private static DialogResult ShowInputDialog(ref string username, ref string password)
        {
            System.Drawing.Size size = new System.Drawing.Size(200, 90); //Formumuzun Boyutu
            Form inputBox = new Form();

            inputBox.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog;
            inputBox.ClientSize = size;
            inputBox.Text = "Name";

            System.Windows.Forms.TextBox usernameBox = new TextBox(); // Username için TextBox
            usernameBox.Size = new System.Drawing.Size(size.Width - 10, 23); // usernameBox kutusunun boyutunu ayarlar
            usernameBox.Location = new System.Drawing.Point(5, 5); // usernameBox kutusunun yerini ayarlar
            usernameBox.Text = username; // Gönderilen username parametresi usernameBox objesinin içerisinde görülecektir.
            inputBox.Controls.Add(usernameBox);

            System.Windows.Forms.TextBox passwordBox = new TextBox();
            passwordBox.Size = new System.Drawing.Size(size.Width - 10, 23);
            passwordBox.Location = new System.Drawing.Point(5, 28);
            passwordBox.Text = password; // Gönderilen password parametresi passwordBox objesinin içerisinde görülecektir.
            inputBox.Controls.Add(passwordBox);

            Button okButton = new Button();
            okButton.DialogResult = System.Windows.Forms.DialogResult.OK;
            okButton.Name = "okButton";
            okButton.Size = new System.Drawing.Size(75, 23);
            okButton.Text = "&OK";
            okButton.Location = new System.Drawing.Point(size.Width - 80 - 80, 54);
            inputBox.Controls.Add(okButton);

            Button cancelButton = new Button();
            cancelButton.DialogResult = System.Windows.Forms.DialogResult.Cancel;
            cancelButton.Name = "cancelButton";
            cancelButton.Size = new System.Drawing.Size(75, 23);
            cancelButton.Text = "&Cancel";
            cancelButton.Location = new System.Drawing.Point(size.Width - 80, 54);
            inputBox.Controls.Add(cancelButton);

            inputBox.AcceptButton = okButton; //Enter tuşuna basıldığında algılar ve okButton butonu işler.
            inputBox.CancelButton = cancelButton; //ESC tuşuna basıldığında algılar ve cancelButton butonu işler.

            DialogResult result = inputBox.ShowDialog();
            username = usernameBox.Text;
            password = passwordBox.Text;
            if (username == "fatih" && password == "zor")
            {
                result = DialogResult.OK;
            }
            else
                result = DialogResult.Cancel;
            return result;
        }
{% endhighlight %}

### Form Load Bölümü

Eğer programımız çalışırken öncelikle bu dialog kutusunu göstermek istiyorsak **Form1_Load** fonksiyonunun ilk satırlarına aşağıdaki kodları belirtmeliyiz.

Form1_Load bölümünde Form1 benim açmış olduğum Form'un ismidir.
{: .notice}

{% highlight c# %}
string username = "Username", password = "Password";

            if (ShowInputDialog(ref username, ref password) == DialogResult.OK)
            {
                MessageBox.Show("Ok");
            }
            else
                MessageBox.Show("Cancel");
{% endhighlight %}
