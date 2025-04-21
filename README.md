import javax.swing.*;
import java.awt.*;
import java.awt.event.*;
import java.util.HashMap;

public class LoginApp {
    private static HashMap<String, String> users = new HashMap<>();

    public static void main(String[] args) {
        SwingUtilities.invokeLater(LoginApp::createAndShowGUI);
    }

    private static void createAndShowGUI() {
        JFrame frame = new JFrame("Login & Create Account");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(400, 300);
        frame.setLocationRelativeTo(null);

        JTabbedPane tabbedPane = new JTabbedPane();

        // Login Tab
        JPanel loginPanel = new JPanel(new GridBagLayout());
        GridBagConstraints gbc = new GridBagConstraints();
        gbc.insets = new Insets(10, 10, 10, 10);
        JTextField loginUser = new JTextField(15);
        JPasswordField loginPass = new JPasswordField(15);
        JButton loginBtn = new JButton("Login");
        JLabel loginMsg = new JLabel();

        gbc.gridx = 0; gbc.gridy = 0; loginPanel.add(new JLabel("Username:"), gbc);
        gbc.gridx = 1; loginPanel.add(loginUser, gbc);
        gbc.gridx = 0; gbc.gridy = 1; loginPanel.add(new JLabel("Password:"), gbc);
        gbc.gridx = 1; loginPanel.add(loginPass, gbc);
        gbc.gridx = 1; gbc.gridy = 2; loginPanel.add(loginBtn, gbc);
        gbc.gridx = 1; gbc.gridy = 3; loginPanel.add(loginMsg, gbc);

        loginBtn.addActionListener(e -> {
            String user = loginUser.getText();
            String pass = new String(loginPass.getPassword());
            if (users.containsKey(user) && users.get(user).equals(pass)) {
                loginMsg.setText("Login Successful! ✨");
                loginMsg.setForeground(Color.GREEN);
            } else {
                loginMsg.setText("Invalid credentials.");
                loginMsg.setForeground(Color.RED);
            }
        });

        // Create Account Tab
        JPanel registerPanel = new JPanel(new GridBagLayout());
        JTextField newUser = new JTextField(15);
        JPasswordField newPass = new JPasswordField(15);
        JButton createBtn = new JButton("Create Account");
        JLabel registerMsg = new JLabel();

        gbc.gridx = 0; gbc.gridy = 0; registerPanel.add(new JLabel("New Username:"), gbc);
        gbc.gridx = 1; registerPanel.add(newUser, gbc);
        gbc.gridx = 0; gbc.gridy = 1; registerPanel.add(new JLabel("New Password:"), gbc);
        gbc.gridx = 1; registerPanel.add(newPass, gbc);
        gbc.gridx = 1; gbc.gridy = 2; registerPanel.add(createBtn, gbc);
        gbc.gridx = 1; gbc.gridy = 3; registerPanel.add(registerMsg, gbc);

        createBtn.addActionListener(e -> {
            String user = newUser.getText();
            String pass = new String(newPass.getPassword());
            if (user.isEmpty() || pass.isEmpty()) {
                registerMsg.setText("Please fill all fields.");
                registerMsg.setForeground(Color.RED);
            } else if (users.containsKey(user)) {
                registerMsg.setText("User already exists.");
                registerMsg.setForeground(Color.RED);
            } else {
                users.put(user, pass);
                registerMsg.setText("Account created successfully! 🎉 i love you crush");
                registerMsg.setForeground(new Color(0, 128, 0));
            }
        });

        tabbedPane.addTab("Login", loginPanel);
        tabbedPane.addTab("Create Account", registerPanel);

        frame.add(tabbedPane);
        frame.setVisible(true);
    }
}
