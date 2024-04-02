<Window x:Class="WpfApp1.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp1"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid Background="#FF565656">
        <ListBox x:Name="list" 
                 HorizontalAlignment="Left"
                 Height="200"
                 Margin="33,0,0,0"
                 VerticalAlignment="Center" 
                 Width="200" 
                 Background="#FFF9F8F8"/>
        <Button Content="Add"
                HorizontalAlignment="Left"
                Margin="33,322,0,0"
                VerticalAlignment="Top"
                Width="84" 
                Click="AddRecord_Click"/>
        <Button Content="Delete" 
                HorizontalAlignment="Left"
                Margin="147,322,0,0" 
                VerticalAlignment="Top" 
                Width="86" 
                Click="DeleteRecord_Click" RenderTransformOrigin="0.07,0.516"/>
        <Button x:Name="btnEdit"
                Content="Edit"
                HorizontalAlignment="Left"
                Height="22"
                Margin="98,347,0,0"
                VerticalAlignment="Top"
                Width="70" Click="Button_Click"/>
    </Grid>
</Window>

ADD WINDOW XAML
<Window x:Class="WpfApp1.AddWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:WpfApp1"
        mc:Ignorable="d"
        Title="AddWindow" Height="450" Width="800">
    <Grid Background="#FF353434">
        <TextBox x:Name="Jmeno"
                 HorizontalAlignment="Left"
                 Height="22" 
                 Margin="56,88,0,0"
                 VerticalAlignment="Top"
                 Width="165"/>
        <Calendar x:Name="kalendar"
                    HorizontalAlignment="Left"
                    Margin="38,202,0,0" 
                    VerticalAlignment="Top" 
                    Width="200"/>
        <Button Content="P idat" 
                HorizontalAlignment="Left"
                Margin="100,375,0,0"
                VerticalAlignment="Top" 
                Width="76"
                Click="Add_Click"/>
        
        
        <TextBlock HorizontalAlignment="Left"
                   Margin="10,88,0,0" 
                   TextWrapping="Wrap" 
                   Text="Jm no" 
                   VerticalAlignment="Top"
                   Width="40"
                   Height="19" Foreground="#FFFDFCFC"/>
        
        
    </Grid>
</Window>
ADDWINDOW XAML CS
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Shapes;

namespace WpfApp1
{
    public partial class AddWindow : Window
    {
        public AddWindow()
        {
            InitializeComponent();
        }

        public string GetRecord()
        {
            string text = Jmeno.Text;
            string date = kalendar.SelectedDate?.ToShortDateString();
            return $"Kniha: {text}DATUM: {date}";
        }

        private void Add_Click(object sender, RoutedEventArgs e)
        {
            DialogResult = true;
        }
    }
}

MAINWINDOW XAML CS
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace WpfApp1
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void AddRecord_Click(object sender, RoutedEventArgs e)
        {
            AddWindow addRecordWindow = new AddWindow();
            if (addRecordWindow.ShowDialog() == true)
            {
                list.Items.Add(addRecordWindow.GetRecord());
            }
        }

        private void DeleteRecord_Click(object sender, RoutedEventArgs e)
        {
            if (list.SelectedItem != null)
            {
                list.Items.Remove(list.SelectedItem);
            }
        }

        private void btnEdit_Click(object sender, RoutedEventArgs e)
        {
            if (list.SelectedIndex != -1) 
            {
                AddWindow editRecordWindow = new AddWindow(list.SelectedItem.ToString());
                if (editRecordWindow.ShowDialog() == true)
                {
                    list.Items[list.SelectedIndex] = editRecordWindow.GetRecord();
                }
            }
        }
    }
}



