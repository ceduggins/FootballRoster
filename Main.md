# FootballRoster


       public frmMain()
        {
         List<Player> _FootballRoster = new List<Player>(10);
          string sort;
            InitializeComponent();
        }
        private void txtName_TextChanged(object sender, EventArgs e)
        {
        }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            AcceptButton = btnAdd;
            btnDisplay.Enabled = true;
            btnAdd.Enabled = false;

            double height = double.Parse(txtHeight.Text);
            double weight = double.Parse(txtWeight.Text);
            double salary = double.Parse(txtSalary.Text);
            DateTime birthday = DateTime.Parse(txtBDay.Text);

            if (rbCanCurr.Checked)
            {
                height = (height / 39.3701);
                weight = (weight / 2.204622);
                salary = (salary * 1.31);
            }
            _FootballRoster.Add(new Player(txtName.Text, txtTeam.Text, birthday, height, weight, salary));

        }
        private void ClearControls()
        {
            txtName.Text = string.Empty;
            txtTeam.Text = string.Empty;
            txtBDay.Text = string.Empty;
            txtHeight.Text = string.Empty;
            txtWeight.Text = string.Empty;
            txtSalary.Text = string.Empty;
            txtDisplay.Text = string.Empty;

            _FootballRoster.Clear();
        }

        private void gbNewPlayer_Enter(object sender, EventArgs e)
        {

        }
        

        private void btnDisplay_Click(object sender, EventArgs e)
        {
            btnDisplay.Enabled = false;

            txtDisplay.AppendText(" -- ROSTER--" + "\n" + _FootballRoster.Count + "\r\n");
            txtDisplay.AppendText("SORTED BY: " + "\n" + sort + "\r\n" + "\r\n");

            RosterDisplay();
            foreach (Player p in _FootballRoster)
            {
                txtDisplay.Text += "Name:" + p.Name + "\r\n";
                txtDisplay.Text += "Team" + p.Team + "\r\n";
                txtDisplay.Text += "Birthday:" + Convert.ToString(p.Birthday) + "\r\n";
                txtDisplay.Text += "Height" + Convert.ToString(p.Height) + "\r\n";
                txtDisplay.Text += "Weight: " + Convert.ToString(p.Weight) + "\r\n";
                txtDisplay.Text += "Salary: " + Convert.ToString(p.Salary) + "\r\n" + "\r\n";
            }
        }


        private void btnDataFill_Click(object sender, EventArgs e)
        {
            btnDataFill.Enabled = false;

            if (_FootballRoster == null) { _FootballRoster = new List<Player>(); }

            Player p = new Player("Joshua Withers", "Baltimore Ravens", DateTime.Parse("01/24/1986"), 200, 62, 150000);
            _FootballRoster.Add(p);
            p = new Player("Lord Farquad", "New England Patriots", DateTime.Parse("05/24/1990"), 250, 42, 856243);
            _FootballRoster.Add(p);
            p = new Player("Paul Martin", "Pittsburgh Steelers", DateTime.Parse("10/27/1971"), 176, 58, 987654);
            _FootballRoster.Add(p);
            p = new Player("Michael Meyers", "New York Giants", DateTime.Parse("03/24/1965"), 160, 60, 111111);
            _FootballRoster.Add(p);
            p = new Player("Christian Grey", "San Francisco 49ers", DateTime.Parse("08/02/1992"), 202, 56, 300000);
            _FootballRoster.Add(p);

            RosterDisplay();
        }

        private void RosterDisplay()
        {
            StringBuilder roster = new StringBuilder();
            foreach (Player p in _FootballRoster)
            {
                roster.AppendLine("Name:" + p.Name);
                roster.AppendLine("Team:" + p.Team);
                roster.AppendLine("Birthday:" + p.Birthday.ToShortDateString());
                roster.AppendLine("Weight:" + p.Weight);
                roster.AppendLine("Height:" + p.Height);
                roster.AppendLine("Salary:" + p.Salary );
            }
            txtDisplay.AppendText(roster.ToString());
        }

        private void btnHeight_Click(object sender, EventArgs e)
        {
            if (sender == btnHeight)
            {
                _FootballRoster = _FootballRoster.OrderBy(x => x.Height).ToList();
                sort = "Height";
            }
        }
        private void btnName_Click(object sender, EventArgs e)
        {
            if (sender == btnName)
                _FootballRoster = _FootballRoster.OrderBy(x => x.Name).ToList();
            sort = "Name";
        }
        private void btnTeam_Click(object sender, EventArgs e)
        {
            if (sender == btnTeam)
                _FootballRoster = _FootballRoster.OrderBy(x => x.Team).ToList();
            sort = "Team";
        }
        private void btnBirthday_Click(object sender, EventArgs e)
        {
            if (sender == btnBirthday)
                _FootballRoster = _FootballRoster.OrderBy(x => x.Team).ToList();
            sort = "Birthday";
        }
        private void btnWeight_Click(object sender, EventArgs e)
        {
            if (sender == btnWeight)
                _FootballRoster = _FootballRoster.OrderBy(x => x.Weight).ToList();
            sort = "Weight";
        }
        private void btnSalary_Click(object sender, EventArgs e)
        {
            if (sender == btnSalary)
                _FootballRoster = _FootballRoster.OrderBy(x => x.Salary).ToList();
            sort = "Salary";
        }

        private void btnClose_Click(object sender, EventArgs e)
        {
            CancelButton = btnClose;
            this.Close();
        }
        private void rbUSACurr_CheckedChanged(object sender, EventArgs e)
        {


        }
        private void rbCanCur_CheckedChanged(object sender, EventArgs e)
        {


        }
        private void btnClear_Click(object sender, EventArgs e)
        {
            ClearControls();
            btnAdd.Enabled = true;
            btnDisplay.Enabled = false;

        }



    }
}
