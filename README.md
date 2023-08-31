import javax.swing.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.DecimalFormat;

public class CurrencyConverter extends JFrame {
    private JComboBox<String> fromCurrencyCombo, toCurrencyCombo;
    private JTextField amountTextField, convertedTextField;
    private JButton convertButton, resetButton, exitButton;

    private String[] currencyUnits = {
        "Units",
        "US Dollar",
        "Nigerian Naira",
        "Brazilian Real",
        "Canadian Dollar",
        "Kenyan Shilling",
        "Indonesian Rupiah",
        "Indian Rupee",
        "Philippine Pisco",
        "Pakistani Rupee"
    };

    private double[] conversionRates = {
        1.0,
        1.31,
        476.57,
        5.47,
        1.71,
        132.53,
        19554.94,
        95.21,
        71.17,
        162.74
    };

    public CurrencyConverter() {
        initComponents();
    }

    private void initComponents() {
        setTitle("Currency Converter");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        fromCurrencyCombo = new JComboBox<>(currencyUnits);
        toCurrencyCombo = new JComboBox<>(currencyUnits);
        amountTextField = new JTextField(10);
        convertedTextField = new JTextField(10);
        convertedTextField.setEditable(false);
        convertButton = new JButton("Convert");
        resetButton = new JButton("Reset");
        exitButton = new JButton("Exit");

        JPanel panel = new JPanel();
        panel.add(new JLabel("From Currency:"));
        panel.add(fromCurrencyCombo);
        panel.add(new JLabel("To Currency:"));
        panel.add(toCurrencyCombo);
        panel.add(new JLabel("Amount:"));
        panel.add(amountTextField);
        panel.add(new JLabel("Converted Amount:"));
        panel.add(convertedTextField);
        panel.add(convertButton);
        panel.add(resetButton);
        panel.add(exitButton);

        add(panel);

        convertButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                convertCurrency();
            }
        });

        resetButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                resetFields();
            }
        });

        exitButton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.exit(0);
            }
        });
    }

    private void convertCurrency() {
        try {
            int fromIndex = fromCurrencyCombo.getSelectedIndex();
            int toIndex = toCurrencyCombo.getSelectedIndex();
            double amount = Double.parseDouble(amountTextField.getText());
            
            double convertedAmount = amount * conversionRates[toIndex] / conversionRates[fromIndex];
            DecimalFormat decimalFormat = new DecimalFormat("#.##");
            convertedTextField.setText(decimalFormat.format(convertedAmount));
        } catch (NumberFormatException ex) {
            JOptionPane.showMessageDialog(this, "Invalid input. Please enter a valid amount.");
        }
    }

    private void resetFields() {
        fromCurrencyCombo.setSelectedIndex(0);
        toCurrencyCombo.setSelectedIndex(0);
        amountTextField.setText("");
        convertedTextField.setText("");
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            @Override
            public void run() {
                new CurrencyConverter().setVisible(true);
            }
        });
    }
}
