create table regforms
(
id int identity(1,1) primary key,
name varchar(20),
email varchar(20),
pass varchar(20),
confpass varchar(20),
phone varchar(10),
gen varchar(10),
address varchar(100)
)
select *from regforms
insert into regforms values('karthi','karthick@gmail.com','karthick@1','karthick@1',6379668248,'male','palayam')

create procedure sp_reg
(
@Name varchar(20),
@Email varchar(20),
@Pass varchar(20),
@Confpass varchar(20),
@Phone varchar(20),
@Gen varchar(10),
@Address varchar(100)
)
as 
begin 
insert into regforms(name,email,pass,confpass,phone,gen,address) values(@Name,@Email,@Pass,@Confpass,@Phone,@Gen,@Address)
end
select *from regforms
================================================================================================================================================
            SqlConnection con = new SqlConnection("Data Source=DESKTOP-2JFC7AR;Integrated Security=true;Initial Catalog=registerpage");
            con.Open();
            SqlCommand com = new SqlCommand();
            com.Connection = con;
            com.CommandType = CommandType.StoredProcedure;
            com.CommandText = "sp_reg";
            com.Parameters.AddWithValue("@Name", txt_name.Text.ToString());
            com.Parameters.AddWithValue("@Phone", txt_num.Text.ToString());
            com.Parameters.AddWithValue("@Email", txt_email.Text.ToString());
            com.Parameters.AddWithValue("@Address", txt_address.Text.ToString());
            com.Parameters.AddWithValue("@Pass", txt_password.Text.ToString());
            com.Parameters.AddWithValue("@Confpass", txt_confpassword.Text.ToString());
            com.Parameters.AddWithValue("@Gen", txt_dropdownlist.Text.ToString());
            int k = com.ExecuteNonQuery();
            if (k != 0)
            {
                lbl_msg.Visible = true;
                lbl_msg.Text = "Records are Submit successfully";
            }
            con.Close();
=======================================================================================================================================================
<%@ Page Language="C#" AutoEventWireup="true" CodeBehind="regs.aspx.cs" Inherits="WebApplication1.regs" %>

<!DOCTYPE html>

<html xmlns="http://www.w3.org/1999/xhtml">
<head runat="server">
    <title></title>
   
    
   
    <style type="text/css">
        .auto-style1 {
            height: 40px;
        }
        .auto-style3 {
            height: 54px;
            width: 365px;
        }
        .auto-style4 {
            height: 708px;
            width: 940px;
        }
        .auto-style5 {
            height: 40px;
            width: 679px;
        }
        .auto-style6 {
            height: 40px;
            width: 365px;
        }
        .auto-style9 {
            width: 440px;
        }
        .auto-style10 {
            height: 40px;
            width: 440px;
        }
        .auto-style11 {
            height: 54px;
            width: 440px;
        }
    </style>
   
    
   
</head>
<body>
    <form id="form1" runat="server">
        <table align="center" class="auto-style4" >
        <tr>
           <td colspan="2" align="center" class="auto-style1">
               <h2>Registration Form</h2></td>
           
        </tr>
        <tr>
            <td class="auto-style3" >
                <b>First Name:</b>
            </td>
            <td class="auto-style10">
                <asp:TextBox ID="txt_name" runat="server" Height="30px" Width="193px"></asp:TextBox>
                <asp:RequiredFieldValidator ID="RequiredFieldValidator2" runat="server" ControlToValidate="txt_name" Display="Dynamic" ErrorMessage="please fill the value" ForeColor="Red" SetFocusOnError="True"></asp:RequiredFieldValidator>
            </td>
        </tr>
        <tr>
            <td class="auto-style3"><b>Email ID:</b></td>
            <td class="auto-style10">
                <asp:TextBox ID="txt_email" runat="server" Height="30px" Width="193px"></asp:TextBox>
                <asp:RegularExpressionValidator ID="RegularExpressionValidator1" runat="server" ControlToValidate="txt_email" Display="Dynamic" ErrorMessage="please enter correct vaue" ForeColor="Red" SetFocusOnError="True" ValidationExpression="\w+([-+.']\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*"></asp:RegularExpressionValidator>
            </td>
        </tr>
        <tr>
            <td class="auto-style3">Gender<b>:</b></td>
            <td class="auto-style11">
                <asp:DropDownList ID="txt_dropdownlist" runat="server" Height="30px" Width="193px">
                    <asp:ListItem Value="0">--select--</asp:ListItem>
                    <asp:ListItem Value="1">Male</asp:ListItem>
                    <asp:ListItem Value="2">Female</asp:ListItem>
                    <asp:ListItem Value="3">Others</asp:ListItem>
                </asp:DropDownList>
            </td>
        </tr>
        <tr>
            <td class="auto-style3">Address<b>:</b></td>
            <td class="auto-style9">
                <asp:TextBox ID="txt_address" runat="server" Height="30px" Width="193px" CssClass="auto-style5" TextMode="MultiLine"></asp:TextBox>
                <asp:RequiredFieldValidator ID="RequiredFieldValidator1" runat="server" BorderStyle="None" ControlToValidate="txt_address" Display="Dynamic" ErrorMessage="please fill the value" ForeColor="Red" SetFocusOnError="True"></asp:RequiredFieldValidator>
            </td>
        </tr>
        <tr>
            <td class="auto-style6"><b>Phone Number:</b></td>
            <td class="auto-style10">
                <asp:TextBox ID="txt_num" runat="server" Height="30px" Width="193px" CssClass="auto-style5" TextMode="Number"></asp:TextBox>
            </td>
        </tr>
        <tr>
            <td class="auto-style3">Password<b>:</b></td>
            <td class="auto-style10">
                <asp:TextBox ID="txt_password" runat="server" Height="30px" Width="193px" TextMode="Password"></asp:TextBox>
            </td>
        </tr>
        <tr>
            <td class="auto-style3">Confirm<b> password:</b></td>
            <td class="auto-style9">
                <asp:TextBox ID="txt_confpassword" runat="server" Height="30px" Width="193px" TextMode="Password"></asp:TextBox>
                <asp:CompareValidator ID="CompareValidator1" runat="server" ControlToCompare="txt_password" ControlToValidate="txt_confpassword" Display="Dynamic" ErrorMessage="does not match" ForeColor="Red" SetFocusOnError="True"></asp:CompareValidator>
            </td>
        </tr>
        <tr>
            <td colspan="2" align="center" class="auto-style1">
                <asp:Button ID="btn_submit" runat="server" Text="Register" ForeColor="Black" Width="105px" Font-Bold="True" Font-Size="Medium" BackColor="#FF3300" OnClick="Btn_submit_Click" />
                <asp:Label ID="lbl_msg" runat="server"></asp:Label>
            </td>
            
        </tr>
        
    </table>
        <div>
        </div>
    </form>
</body>
</html>
===================================
login

         try
            {
                SqlConnection con = new SqlConnection("Data Source=DESKTOP-2JFC7AR;Integrated Security=true;Initial Catalog=registerpage");
                SqlDataAdapter sda = new SqlDataAdapter("SELECT COUNT(*) FROM  regforms WHERE email='" + txt_email.Text + "' AND pass='" + txt_pass.Text + "'", con);
                DataTable dt = new DataTable();
                sda.Fill(dt);
                if (dt.Rows[0][0].ToString() == "1")
                {
                    Response.Redirect("regs.aspx");

                }
            }
            catch
            {
                {
                    lbl.Text = "Login Unsuccessfull";
                }
            }
        }
         
