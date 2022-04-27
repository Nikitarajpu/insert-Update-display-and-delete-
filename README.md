# insert-Update-display-and-delete-
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Windows.Forms;
using System.Data.SqlClient;

namespace WindowsFormsApplication14
{
    public partial class Form1 : Form
    {
        SqlConnection con = new SqlConnection();
        public Form1()
        {
            InitializeComponent();
            disp_Click();
            con.ConnectionString = "Data Source=.;Initial Catalog=emp123;Integrated Security=True;Pooling=False";
           // con.Open();

        }

        private void btnsave_Click(object sender, EventArgs e)
        {
            SqlCommand cmd = new SqlCommand("insert into emp123 values('"+int.Parse(tid.Text)+"','"+t2.Text+"')",con);
            cmd.ExecuteNonQuery();
            MessageBox.Show("inserted ");
         

        }

        private void button1_Click(object sender, EventArgs e)
        {
            SqlCommand cmd = new SqlCommand("update emp123 set ename='"+t2.Text+"' where eid='"+int.Parse(tid.Text)+"'",con);
            cmd.ExecuteNonQuery();
            
           
            MessageBox.Show("updated");
            con.Open();
            con.Close();
            disp_Click();

        }

        private void disp_Click()
        {

            DataTable dt = new DataTable();
            SqlDataAdapter adt = new SqlDataAdapter("select *from emp123", con);
            adt.Fill(dt);
            dataGridView2.DataSource = dt;
            con.Open();
            con.Close();
        }

        private void Form1_Load(object sender, EventArgs e)
        {
            // TODO: This line of code loads data into the 'emp123DataSet.emp123' table. You can move, or remove it, as needed.
            this.emp123TableAdapter.Fill(this.emp123DataSet.emp123);

        }
      /*  private void Display()
        {
            DataTable dt = new DataTable();
            SqlDataAdapter adt = new SqlDataAdapter("select *from emp123 where eid='" + int.Parse(tid.Text) + "' ", con);
            dataGridView1.DataSource = adt.Fill(dt);
        }*/
        private void dataGridView1_RowHeaderMouseClick(object sender, DataGridViewCellMouseEventArgs e)
        {
            tid.Text = dataGridView1.Rows[e.RowIndex].Cells[0].Value.ToString();
            t2.Text = dataGridView1.Rows[e.RowIndex].Cells[1].Value.ToString();
        }

        private void del_Click(object sender, EventArgs e)
        {
            SqlCommand cmd = new SqlCommand("delete from emp123 where eid='" + int.Parse(tid.Text) + "'", con);
            cmd.ExecuteNonQuery();
            MessageBox.Show("deleted ");
        }

        private void dataGridView2_CellContentClick(object sender, DataGridViewCellEventArgs e)
        {
            tid.Text = dataGridView2.Rows[e.RowIndex].Cells[0].Value.ToString();
            t2.Text = dataGridView2.Rows[e.RowIndex].Cells[1].Value.ToString();
        }

        private void timer1_Tick(object sender, EventArgs e)
        {
            this.dataGridView1.Refresh();
            this.dataGridView1.Parent.Refresh();
        }
    }
}
