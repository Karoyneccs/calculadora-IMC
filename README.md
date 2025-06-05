import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class CalculadoraIMC extends JFrame {

    private JTextField pesoField, alturaField;
    private JButton calcularButton;
    private JLabel resultadoLabel;

    public CalculadoraIMC() {
        super("Calculadora de IMC");

        
        setLayout(new GridLayout(5, 2, 5, 5));

        
        add(new JLabel("Peso (Kg):"));
        pesoField = new JTextField();
        add(pesoField);

        add(new JLabel("Altura (Cm):"));
        alturaField = new JTextField();
        add(alturaField);

        calcularButton = new JButton("Calcular IMC");
        add(calcularButton);

        resultadoLabel = new JLabel("Informe os dados e clique em Calcular.");
        add(resultadoLabel);

        
        calcularButton.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                calcularIMC();
            }
        });

        
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setSize(350, 200);
        setLocationRelativeTo(null);
        setVisible(true);
    }

    private void calcularIMC() {
        try {
            double peso = Double.parseDouble(pesoField.getText().replace(",", "."));
            double alturaCm = Double.parseDouble(alturaField.getText().replace(",", "."));
            double alturaM = alturaCm / 100;

            if (peso <= 0 || alturaCm <= 0) {
                resultadoLabel.setText("Peso e altura devem ser maiores que zero.");
                return;
            }

            double imc = peso / (alturaM * alturaM);
            String classificacao = classificarIMC(imc);

            resultadoLabel.setText(String.format("IMC: %.2f - %s", imc, classificacao));
        } catch (NumberFormatException ex) {
            resultadoLabel.setText("Por favor, informe valores numéricos válidos.");
        }
    }

    private String classificarIMC(double imc) {
        if (imc < 18.5) {
            return "Abaixo do peso";
        } else if (imc < 25) {
            return "Peso normal";
        } else if (imc < 30) {
            return "Sobrepeso";
        } else if (imc < 35) {
            return "Obesidade grau I";
        } else if (imc < 40) {
            return "Obesidade grau II";
        } else {
            return "Obesidade grau III (mórbida)";
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> new CalculadoraIMC());
    }
}
