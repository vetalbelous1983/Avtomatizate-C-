# hello-world Me first Code
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;
using OpenQA.Selenium;
using OpenQA.Selenium.Support.UI;




namespace Vetal_Form2
{
    public partial class Form1 : Form
    {
        IWebDriver Browser;

        public Form1()
        {
            InitializeComponent();
        }
        //Первый урок Lessons 1
        private void button1_Click(object sender, EventArgs e)
        {
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
            Browser.Manage().Window.Maximize();
            Browser.Navigate().GoToUrl("https://google.com");

            IWebElement SearchInput = Browser.FindElement(By.Name("q"));
            SearchInput.SendKeys("Что означает имя Виталий" + OpenQA.Selenium.Keys.Enter);
        }

        private void button2_Click(object sender, EventArgs e)
        {
            Browser.Close();
            Browser.Quit();

        }

        private void Form1_Load(object sender, EventArgs e)
        {

        }
        //Lessons 2 Button 4 and Button 3 
        private void button4_Click(object sender, EventArgs e)
        {
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
            Browser.Manage().Window.Maximize();
            Browser.Navigate().GoToUrl("http://sportmir.dp.ua/");

        }

        private void button3_Click(object sender, EventArgs e)
        {
            IWebElement element;
            //Поиск с Google
            // element = Browser.FindElement(By.Name("q"));
            // element.SendKeys("Vetal Молодец");

            element = Browser.FindElement(By.ClassName("banner_input"));
            element.Click();
            element.SendKeys("Vetal Молодец");



            //Поиск по полному ссылки тексту
            // element = Browser.FindElement( By.LinkText("Блог"));
            // element.Click();


            // Поиск по частичному тексту ссылки
            //element = Browser.FindElement( By.PartialLinkText("правочн"));
            //element.Click();

        }

        // Lesson 3 and 4


        private void button5_Click(object sender, EventArgs e)
        {
            List<IWebElement> News = Browser.FindElements(By.CssSelector("#pillmenu a")).ToList();
            for (int i = 0; i < News.Count; i++)
            {
                textBox1.AppendText(News[i].Text + "\r\n");
            }
        }

        private void button6_Click(object sender, EventArgs e)
        {
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
            Browser.Manage().Window.Maximize();
            Browser.Navigate().GoToUrl("http://www.utmk-v1.dump.dp.ua/");
        }

        private void button8_Click(object sender, EventArgs e)
        {
            {
                List<IWebElement> News = Browser.FindElements(By.CssSelector("#pillmenu a")).ToList();
                for (int i = 0; i < News.Count; i++)
                {
                    String s = News[i].Text;

                    if (s.StartsWith("ЮМОР"))
                    {
                        textBox1.AppendText("Новость №" + (i + 1).ToString() + "Начинаются с текста 'Ю'" + "\r\n");

                    }
                    if (s.EndsWith("ЗАНИМАЕТСЯ?"))
                    {
                        textBox1.AppendText("Новость №" + (i + 1).ToString() + "Заканчивается с текста 'Занимается'" + "\r\n");
                    }
                    if (s.Contains("ДНЁМ"))
                    {
                        textBox1.AppendText("Новость №" + (i + 1).ToString() + "Содержит с текста 'Днем'" + "\r\n");
                        News[i].Click();
                        break;
                    }
                }

            }
        }

        //Урок 5

        private void button9_Click(object sender, EventArgs e)
        {
            IJavaScriptExecutor jse = Browser as IJavaScriptExecutor;
            jse.ExecuteScript(textBox1.Text);
            //Необходимо Вставить в Текст Бокс (textBox1)
            //$(".news-preview-image").fadeOut(8000);
             // $(".news-preview-image").fadeIn();*/
            //Необходимо Или такое вставить Одно и тоже
            //$(".news-preview-image").hide(8000);
            // $(".news-preview-image").show();*/
        }

        private void button10_Click(object sender, EventArgs e)
        {
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
            Browser.Manage().Window.Maximize();
            Browser.Navigate().GoToUrl("https://securitymedia.dump.dp.ua/");
        }
        //Урок 6
        private void button12_Click(object sender, EventArgs e)
        {
            Browser.SwitchTo().Window(Browser.WindowHandles[0]);
            System.Windows.Forms.MessageBox.Show(Browser.Title + "\r\n" + Browser.Url);

            Browser.SwitchTo().Window(Browser.WindowHandles[2]);
            System.Windows.Forms.MessageBox.Show(Browser.Title + "\r\n" + Browser.Url);

            Browser.SwitchTo().Window(Browser.WindowHandles[1]);
            System.Windows.Forms.MessageBox.Show(Browser.Title + "\r\n" + Browser.Url);
        }

        //Урок 7

        private void button13_Click(object sender, EventArgs e)
        {
            /* Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
             Browser.Manage().Window.Maximize();*/
            Browser.Navigate().GoToUrl("https://www.degraeve.com/reference/simple-ajax-example.php");

            IWebElement Button = Browser.FindElement(By.CssSelector("Input[value='Go']"));
            Button.Click();

            System.Threading.Thread.Sleep(7000);
            //Browser.Manage().Timeouts().ImplicitWait(TimeSpan.FromSeconds(10));

            IWebElement txt = Browser.FindElement(By.CssSelector("#result p"));
            textBox1.Text = txt.Text;

        }
        //Лишняя вторая 2 кнопка закрыть браузер
        private void button11_Click(object sender, EventArgs e)
        {
            Browser.Close();
            Browser.Quit();
        }

        //8 ой Урок последний

        IWebElement GetElement(By locator)
        {
        List<IWebElement> elements = Browser.FindElements(locator).ToList();
        if (elements.Count > 0) return elements[0];
        else return null;
        }

        private void button14_Click(object sender, EventArgs e)
        {
            Browser = new OpenQA.Selenium.Chrome.ChromeDriver();
            Browser.Manage().Window.Maximize();
            Browser.Navigate().GoToUrl("http://www.seosprint.net/");

            //IWebElement login = Browser.FindElement(By.ClassName("gopa"));
            //IWebElement login = GetElement(By.ClassName("gopa"));
            IWebElement login = GetElement(By.ClassName("btnlogin")); 
            if (login != null)
            {
                login.Click();
            }
        }
    }
}
