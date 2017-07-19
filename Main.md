# FootballRoster

 public frmMain()
        {
            InitializeComponent();
            
            List<Player> _FootballRoster = new List<Player>();
        }

        private void btnAdd_Click(object sender, EventArgs e)
        {
            AcceptButton = btnAdd;
            btnAdd.Enabled = false;

            frmAddNewPlayer np = new frmAddNewPlayer();
            if (np.ShowDialog() == DialogResult.OK)
            {
                Player p = new Player();
                p = (Player)np.Tag;
                _FootballRoster.Add(p);
                BindData();
            }
        }

        private void btnDataFill_Click(object sender, EventArgs e)
        {
            btnDataFill.Enabled = false;
            _FootballRoster.Add(new Player("Jim Brown", "Cleveland Browns", new DateTime (1936, 02, 17), 232, 74, 65000));
            _FootballRoster.Add(new Player("Deion Sanders", "Baltimore Ravens", new DateTime(1967, 08, 09), 192, 73, 1300000));
            _FootballRoster.Add(new Player("Odell Beckham", "New York Giants", new DateTime(1992, 11, 05), 194, 72, 1839027));
            _FootballRoster.Add(new Player("Troy Polamalu", "Pittsburgh Steelers", new DateTime(1981, 04, 19), 207, 71.5, 11750000));
            _FootballRoster.Add(new Player("Micheal Vick", "Atlanta Falcons", new DateTime(1980, 06, 26), 216, 72, 7600000));

            BindData();
        }
        private void LoadDetails()
        { 
           if (dgvRoster.SelectedRows.Count == 0) { return; }
                Player p = (Player) dgvRoster.SelectedRows[0].DataBoundItem;

                txtName.Text = p.Name;
                txtTeam.Text = p.Team;
                txtBirthday.Text = (p.Birthday.ToShortDateString());
                txtHeight.Text  = (p.Height.ToString());
                txtWeight.Text = (p.Weight.ToString());
                txtSalary.Text = (p.Salary.ToString("c"));
            
            
        }

        private void BindData()
        {
            dgvRoster.DataSource = typeof(List<Player>);
            dgvRoster.DataSource = _FootballRoster; 
            AdjustColumnOrder();
        }
  
        private void AdjustColumnOrder()
        {
            dgvRoster.Columns["Name"].DisplayIndex = 0;
            dgvRoster.Columns["Team"].DisplayIndex = 1;
            dgvRoster.Columns["Birthday"].DisplayIndex = 2;
            dgvRoster.Columns["Height"].DisplayIndex = 3;
            dgvRoster.Columns["Weight"].DisplayIndex = 4;
            dgvRoster.Columns["Salary"].DisplayIndex = 5;

           
        }

        private void ClearControls()
        {
            txtName.Text = string.Empty;
            txtTeam.Text = string.Empty;
            txtBirthday.Text = string.Empty;
            txtHeight.Text = string.Empty;
            txtWeight.Text = string.Empty;
            txtSalary.Text = string.Empty;
            gbSortBy.BackColor = DefaultBackColor;
            _FootballRoster.Clear();
        }
        private void SetButtons(ref GroupBox GBX , Button btn)
        {
  
            foreach (Button b in GBX.Controls)
            {
                if (b.Name == btn.Name)
                {
                    b.BackColor = Color.LightGreen;
                }
                else
                {
                    b.BackColor = DefaultBackColor;
                }
            }
        }
        
        private void btnName_Click(object sender, EventArgs e)
        { 
            if (sender == btnName)
            {
              
                _FootballRoster = _FootballRoster.OrderBy(x => x.Name).ToList();   
            }

            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Name).ToList();


            SetButtons(ref gbSortBy, sender as Button);
            BindData();
        }

        private void btnTeam_Click(object sender, EventArgs e)
        {
            if (sender == btnTeam)
            {
                
                _FootballRoster = _FootballRoster.OrderBy(x => x.Team).ToList();
                
            }
            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Team).ToList();


            SetButtons(ref gbSortBy, sender as Button);
            
        }
        private void btnBDay_Click(object sender, EventArgs e)
        {
            
            if (sender == btnBDay)
            {
                
                _FootballRoster = _FootballRoster.OrderBy(x => x.Birthday).ToList();
               
            }
            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Birthday).ToList();

            SetButtons(ref gbSortBy, sender as Button);
           
        }

        private void btnHeight_Click(object sender, EventArgs e)
        {
           
            if (sender == btnHeight)
            {
                
                _FootballRoster = _FootballRoster.OrderBy(x => x.Height).ToList();
            }
            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Height).ToList();


            SetButtons(ref gbSortBy, sender as Button);
            BindData();
        }

        private void btnWeight_Click(object sender, EventArgs e)
        {
            
            if (sender == btnWeight)
            {
               
                _FootballRoster = _FootballRoster.OrderBy(x => x.Weight).ToList();
            }
            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Weight).ToList();


            SetButtons(ref gbSortBy, sender as Button);
            BindData();
        }

        private void btnSalary_Click(object sender, EventArgs e)
        {
            if (sender == btnSalary)
            {
                
                _FootballRoster = _FootballRoster.OrderBy(x => x.Salary).ToList();
            }
            _FootballRoster = _FootballRoster.OrderByDescending(x => x.Salary).ToList();


            SetButtons(ref gbSortBy, sender as Button);
            BindData();
        }

        private void frmMain_Load(object sender, EventArgs e)
        {

            _FootballRoster = new List<Player>();
            BindData();
        }
    
        private void btnClose_Click(object sender, EventArgs e)
        {
            this.Close();
            BindData();
        }

        private void btnClear_Click(object sender, EventArgs e)
        {
            ClearControls();
            btnAdd.Enabled = true;
            BindData();
        }

        private void dgvRoster_SelectionChanged(object sender, EventArgs e)
        {
            LoadDetails();
        }

        private void dgvRoster_CellFormatting(object sender, DataGridViewCellFormattingEventArgs e)
        {
            if (e.ColumnIndex == dgvRoster.Columns["Height"].Index && e.RowIndex != this.dgvRoster.NewRowIndex)
            {
                double inches = (double)(e.Value) % 12;
                double feet = (double)(e.Value) / (12);
                e.Value = Math.Round (feet, 0) + "'" + inches + "''";



            }

        }
    }

