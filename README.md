学生选课系统设计
实验要求
    1）人物属性（编号、姓名、性别、课程等）
    2）GUI窗体
    3）支持学生进行选课操作
    3）能进行常见的异常处理
学生选课系统设计
实验目的
分析学生选课系统
使用GUI窗体及其组件设计窗体界面
完成学生选课过程业务逻辑编程
基于文件保存并读取数据
处理异常


核心代码
GUI：
登陆界面：
public Chose() {
		setTitle("Chose Classes");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 800, 400);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		GridBagLayout gbl_contentPane = new GridBagLayout();
		gbl_contentPane.columnWidths = new int[]{185, 136, 0};
		gbl_contentPane.rowHeights = new int[]{51, 86, 0};
		gbl_contentPane.columnWeights = new double[]{1.0, 0.0, Double.MIN_VALUE};
		gbl_contentPane.rowWeights = new double[]{0.0, 1.0, Double.MIN_VALUE};
		contentPane.setLayout(gbl_contentPane);
		
		Label label = new Label("选课\n\"每次限选一门课程.\"");
		label.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 20));
		GridBagConstraints gbc_label = new GridBagConstraints();
		gbc_label.insets = new Insets(0, 0, 5, 5);
		gbc_label.gridx = 0;
		gbc_label.gridy = 0;
		contentPane.add(label, gbc_label);
		
		DefaultListModel listModel=new DefaultListModel(); //new Model
		JList list = new JList(listModel); // new list
		GridBagConstraints gbc_list = new GridBagConstraints();
		gbc_list.insets = new Insets(0, 0, 0, 5);
		gbc_list.fill = GridBagConstraints.BOTH;
		gbc_list.gridx = 0; // layout
		gbc_list.gridy = 1;
		contentPane.add(list, gbc_list);
		//reader
		try {
            BufferedReader br = new BufferedReader(new FileReader("C:\\Users\\18804\\Desktop\\新建文件夹 (4)\\ep3.txt"));
            String demo = br.readLine();
            br.close();
            String [] demoarray = demo.split(";"); //use ; to split each sentence
            for (int i=0; i<demoarray.length ;i++) {
        		listModel.addElement(demoarray[i]); //roop to add into lists
            }
        } catch (IOException e1) {
            e1.printStackTrace();
        }
		JButton btnNewButton = new JButton("Select");
		GridBagConstraints gbc_btnNewButton = new GridBagConstraints();
		gbc_btnNewButton.gridwidth = 2;
		gbc_btnNewButton.gridx = 1;
		gbc_btnNewButton.gridy = 1;
		contentPane.add(btnNewButton, gbc_btnNewButton);
		btnNewButton.addActionListener(new ActionListener(){
			public void actionPerformed(ActionEvent e) {
				String chosen = (String)list.getSelectedValue()+";"; //Object to String with ";"
				//System.out.println(chosen);
				 FileWriter writer; // writer
			        try {
			            writer = new FileWriter("C:\\Users\\18804\\Desktop\\新建文件夹 (4)\\ep3.txt",true);		            
			            writer.append(chosen); // + append
			            writer.flush();
			            writer.close();
			        } catch (IOException e1) {
			            e1.printStackTrace();
			        }
					JOptionPane.showMessageDialog(null, "选课成功!"); //Tips
				    System.exit(0);
     
选择界面：
public Create() {
		setTitle("课程新加");
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 450, 300);
		contentPane = new JPanel();
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		setContentPane(contentPane);
		GridBagLayout gbl_contentPane = new GridBagLayout();
		gbl_contentPane.columnWidths = new int[]{93, 142, 164, 0};
		gbl_contentPane.rowHeights = new int[]{0, 0, 0, 0, 0, 0, 0, 0, 0};
		gbl_contentPane.columnWeights = new double[]{1.0, 0.0, 0.0, Double.MIN_VALUE};
		gbl_contentPane.rowWeights = new double[]{1.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 1.0, Double.MIN_VALUE};
		contentPane.setLayout(gbl_contentPane);
		
		Label label = new Label("课程编号: ");
		label.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label = new GridBagConstraints();
		gbc_label.insets = new Insets(0, 0, 5, 5);
		gbc_label.gridx = 0;
		gbc_label.gridy = 1;
		contentPane.add(label, gbc_label);
		// Create Label
		TextField textField = new TextField();
		GridBagConstraints gbc_textField = new GridBagConstraints();
		gbc_textField.fill = GridBagConstraints.BOTH;
		gbc_textField.insets = new Insets(0, 0, 5, 5);
		gbc_textField.gridx = 1;
		gbc_textField.gridy = 1;
		contentPane.add(textField, gbc_textField);
		// Create textField
		Label label_1 = new Label("课程名称: ");
		label_1.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label_1 = new GridBagConstraints();
		gbc_label_1.insets = new Insets(0, 0, 5, 5);
		gbc_label_1.gridx = 0;
		gbc_label_1.gridy = 2;
		contentPane.add(label_1, gbc_label_1);
		
		TextField textField_1 = new TextField();
		GridBagConstraints gbc_textField_1 = new GridBagConstraints();
		gbc_textField_1.fill = GridBagConstraints.BOTH;
		gbc_textField_1.insets = new Insets(0, 0, 5, 5);
		gbc_textField_1.gridx = 1;
		gbc_textField_1.gridy = 2;
		contentPane.add(textField_1, gbc_textField_1);
		
		Label label_2 = new Label("上课地点: ");
		label_2.setFont(new Font("Cambria", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label_2 = new GridBagConstraints();
		gbc_label_2.insets = new Insets(0, 0, 5, 5);
		gbc_label_2.gridx = 0;
		gbc_label_2.gridy = 3;
		contentPane.add(label_2, gbc_label_2);
		
		TextField textField_2 = new TextField();
		GridBagConstraints gbc_textField_2 = new GridBagConstraints();
		gbc_textField_2.fill = GridBagConstraints.BOTH;
		gbc_textField_2.insets = new Insets(0, 0, 5, 5);
		gbc_textField_2.gridx = 1;
		gbc_textField_2.gridy = 3;
		contentPane.add(textField_2, gbc_textField_2);
		
		Label label_3 = new Label("上课时间: ");
		label_3.setFont(new Font("Cambria", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label_3 = new GridBagConstraints();
		gbc_label_3.insets = new Insets(0, 0, 5, 5);
		gbc_label_3.gridx = 0;
		gbc_label_3.gridy = 4;
		contentPane.add(label_3, gbc_label_3);
		
		TextField textField_3 = new TextField();
		GridBagConstraints gbc_textField_3 = new GridBagConstraints();
		gbc_textField_3.fill = GridBagConstraints.BOTH;
		gbc_textField_3.insets = new Insets(0, 0, 5, 5);
		gbc_textField_3.gridx = 1;
		gbc_textField_3.gridy = 4;
		contentPane.add(textField_3, gbc_textField_3);
		
		Label label_4 = new Label("学分: ");
		label_4.setFont(new Font("Cambria", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label_4 = new GridBagConstraints();
		gbc_label_4.insets = new Insets(0, 0, 5, 5);
		gbc_label_4.gridx = 0;
		gbc_label_4.gridy = 5;
		contentPane.add(label_4, gbc_label_4);
		
		TextField textField_4 = new TextField();
		GridBagConstraints gbc_textField_4 = new GridBagConstraints();
		gbc_textField_4.fill = GridBagConstraints.BOTH;
		gbc_textField_4.insets = new Insets(0, 0, 5, 5);
		gbc_textField_4.gridx = 1;
		gbc_textField_4.gridy = 5;
		contentPane.add(textField_4, gbc_textField_4);
		
		Label label_5 = new Label("授课教师: ");
		label_5.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 12));
		GridBagConstraints gbc_label_5 = new GridBagConstraints();
		gbc_label_5.insets = new Insets(0, 0, 5, 5);
		gbc_label_5.gridx = 0;
		gbc_label_5.gridy = 6;
		contentPane.add(label_5, gbc_label_5);
		
		TextField textField_5 = new TextField();
		GridBagConstraints gbc_textField_5 = new GridBagConstraints();
		gbc_textField_5.fill = GridBagConstraints.BOTH;
		gbc_textField_5.insets = new Insets(0, 0, 5, 5);
		gbc_textField_5.gridx = 1;
		gbc_textField_5.gridy = 6;
		contentPane.add(textField_5, gbc_textField_5);

		Button button = new Button("创建课程"); //set Button name
		button.setFont(new Font("Calibri", Font.BOLD | Font.ITALIC, 18)); // set font
		GridBagConstraints gbc_button = new GridBagConstraints();
		gbc_button.fill = GridBagConstraints.BOTH; //layout
		gbc_button.gridx = 2;
		gbc_button.gridy = 7; //position
		contentPane.add(button, gbc_button);
		button.addActionListener(new ActionListener(){
			public void actionPerformed(ActionEvent e) {
				String s= textField.getText();
				String s1= textField_1.getText();
				String s2= textField_2.getText();
				String s3= textField_3.getText();
				String s4= textField_4.getText();
				String s5= textField_5.getText(); // get infos
				String s6 = "课程编号: "+ s + " 课程名称: "+ s1 +" 上课地点: "+ s2 +" 上课时间: " + s3 +" 学分: "+ s4 + " 授课老师: "+ s5+ ";"; //add together
				System.out.println(s6);
			    FileWriter writer;
			    // File operate
		        try {

		            writer = new FileWriter("C:\\Users\\18804\\Desktop\\新建文件夹 (4)\\ep3.txt",true);
		            writer.append(s6); // + append 
		            writer.flush();
		            writer.close();
		        } catch (IOException e1) {
		            e1.printStackTrace();
		        }
				JOptionPane.showMessageDialog(null, "创建成功!");
			    System.exit(0);
			}
		});
	}
}
    

在进行文件读取操作：
    JLabel lblNewLabe2 = new JLabel("");   		
   	    contentPane2.add(lblNewLabe2);
        {   
        	DefaultListModel listMode2=new DefaultListModel(); 
        	JList list2 = new JList(listMode2);
        	contentPanel.add(list2);
            String [] demoarray = demo1.split(";");	             
         	listMode2.addElement(demoarray[1]);
        }	        
        JLabel lblNewLabel = new JLabel("选择了以下课程:");
		lblNewLabel.setFont(new Font("微软雅黑", Font.BOLD | Font.ITALIC, 14));
		contentPanel.add(lblNewLabel);
        {   
        	DefaultListModel listModel=new DefaultListModel(); 
        	JList list = new JList(listModel);
        	contentPanel.add(list);
             String [] demoarray = demo.split(";");
             for (int i=0; i<demoarray.length ;i++) {
         		listModel.addElement(demoarray[0]);
             }
        }
        //System.out.println("读取txt文件数据：" + demo);
    } catch (IOException e1) {
        e1.printStackTrace();
    }
  
五、编程感想 上学期曾学过python语言，二者相对比，python在编写简单，但Java相应更快，因此二者不可兼得，最后一个实验融汇了前面所有实验的知识点，
前面有些地方学的不是很好，因此此次实验有部分，像同学进行了借鉴，还参考了csdn上的设计代码，与网上的代码相比，我的没有运用数据库，在大批量数据处理时，会很棘手，
下一步学习一下数据库技术，对其进行进一步优化。
