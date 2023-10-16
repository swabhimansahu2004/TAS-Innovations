import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.*;
import javax.swing.filechooser.FileNameExtensionFilter;
import java.awt.Font;
import java.awt.event.*;
import javax.swing.text.DefaultEditorKit;

public class Basic_Text_Editor{
    private JFrame frame;
    private JTextArea textArea;
    private JFileChooser fileChooser;
    private boolean isTextSaved;
    private JSpinner fontsizespinner;
    private JComboBox<String> fontBox;
    private Font currentFont;

    public Basic_Text_Editor() {
        frame = new JFrame("Basic Text Editor");
        frame.setDefaultCloseOperation(JFrame.DO_NOTHING_ON_CLOSE);
        frame.setSize(800, 600);

        textArea = new JTextArea();
        textArea.setFont(new Font("Arial", Font.PLAIN, 16));
        frame.add(new JScrollPane(textArea), BorderLayout.CENTER);

        fileChooser = new JFileChooser();
        fileChooser.setFileFilter(new FileNameExtensionFilter("Text Files (*.txt)", "txt"));

        JMenuBar menuBar = new JMenuBar();
        JMenu fileMenu = new JMenu("File");
        JMenuItem openItem = new JMenuItem("Open");
        JMenuItem saveItem = new JMenuItem("Save");
        JMenuItem saveAsItem = new JMenuItem("Save As");
        JMenuItem exitItem = new JMenuItem("Exit");
        
        openItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_O, InputEvent.CTRL_DOWN_MASK));
        saveItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK));
        saveAsItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_S, InputEvent.CTRL_DOWN_MASK | InputEvent.SHIFT_DOWN_MASK));
        
        exitItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_X, InputEvent.CTRL_DOWN_MASK | InputEvent.SHIFT_DOWN_MASK));
        exitItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                handleWindowClosing();
            }
        });
        
        openItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                openFile();
            }
        });

        saveItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                saveFile();
            }
        });

        saveAsItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                saveFileAs();
            }
        });

        
        fileMenu.add(openItem);
        fileMenu.addSeparator();
        fileMenu.add(saveItem);
        fileMenu.add(saveAsItem);
        fileMenu.addSeparator();
        fileMenu.add(exitItem);
        
        JMenuItem fontFamilyItem = new JMenuItem("Font Family");
        fontFamilyItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_F, InputEvent.CTRL_DOWN_MASK));
        fontFamilyItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                selectFontFamily();
            }
        });
        
        
        JMenuItem cutItem = new JMenuItem(new DefaultEditorKit.CutAction());
        cutItem.setText("Cut");
        cutItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_X, InputEvent.CTRL_DOWN_MASK));

        JMenuItem copyItem = new JMenuItem(new DefaultEditorKit.CopyAction());
        copyItem.setText("Copy");
        copyItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_C, InputEvent.CTRL_DOWN_MASK));

        JMenuItem pasteItem = new JMenuItem(new DefaultEditorKit.PasteAction());
        pasteItem.setText("Paste");
        pasteItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_V, InputEvent.CTRL_DOWN_MASK));

       
        JToolBar toolbar = new JToolBar();
        JButton boldButton = new JButton("Bold");
        JButton italicButton = new JButton("Italic");

        boldButton.addActionListener(e -> {
            Font currentFont = textArea.getFont();
            Font newFont = new Font(currentFont.getName(), currentFont.getStyle() | Font.BOLD, currentFont.getSize());
            textArea.setFont(newFont);
        });

        italicButton.addActionListener(e -> {
            Font currentFont = textArea.getFont();
            Font newFont = new Font(currentFont.getName(), currentFont.getStyle() | Font.ITALIC, currentFont.getSize());
            textArea.setFont(newFont);
        });

        toolbar.add(boldButton);
        toolbar.add(italicButton);

        frame.add(toolbar, BorderLayout.SOUTH);

        
        
        JMenu editMenu = new JMenu("Edit");
        JMenuItem textSizeItem = new JMenuItem("Text Size");
        JMenuItem textColorItem = new JMenuItem("Text Color");
        
        textSizeItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_T, InputEvent.CTRL_DOWN_MASK));
        textColorItem.setAccelerator(KeyStroke.getKeyStroke(KeyEvent.VK_T, InputEvent.CTRL_DOWN_MASK | InputEvent.SHIFT_DOWN_MASK));

        textSizeItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                int newSize = Integer.parseInt(JOptionPane.showInputDialog(frame, "Enter new text size:"));
                textArea.setFont(new Font(textArea.getFont().getFamily(), textArea.getFont().getStyle(), newSize));
            }
        });

        textColorItem.addActionListener(new ActionListener() {
            public void actionPerformed(ActionEvent e) {
                Color newColor = JColorChooser.showDialog(frame, "Choose Text Color", textArea.getForeground());
                textArea.setForeground(newColor);
            }
        });

        editMenu.add(cutItem);
        editMenu.add(copyItem);
        editMenu.add(pasteItem);
        editMenu.addSeparator();
        editMenu.add(textSizeItem);
        editMenu.add(textColorItem);
        editMenu.add(fontFamilyItem);

        menuBar.add(fileMenu);
        menuBar.add(editMenu);
        frame.setJMenuBar(menuBar);

        frame.addWindowListener(new WindowAdapter() {
            @Override
            public void windowClosing(WindowEvent e) {
                handleWindowClosing();
            }
        });

        frame.setVisible(true);
    }

    private void selectFontFamily() {
        String[] fontFamilies = GraphicsEnvironment.getLocalGraphicsEnvironment().getAvailableFontFamilyNames();
        String selectedFontFamily = (String) JOptionPane.showInputDialog(frame, "Select Font Family:", "Font Family",
                JOptionPane.PLAIN_MESSAGE, null, fontFamilies, textArea.getFont().getFamily());

        if (selectedFontFamily != null) {
            Font currentFont = textArea.getFont();
            textArea.setFont(new Font(selectedFontFamily, currentFont.getStyle(), currentFont.getSize()));
        }
    }

    private void openFile() {
        int returnValue = fileChooser.showOpenDialog(null);
        if (returnValue == JFileChooser.APPROVE_OPTION) {
            File selectedFile = fileChooser.getSelectedFile();
            try {
                BufferedReader reader = new BufferedReader(new FileReader(selectedFile));
                textArea.read(reader, null);
                reader.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    private void saveFile() {
        if (fileChooser.getSelectedFile() == null) {
            saveFileAs();
            return;
        }

        try {
            BufferedWriter writer = new BufferedWriter(new FileWriter(fileChooser.getSelectedFile()));
            textArea.write(writer);
            writer.close();
            isTextSaved = true;
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private void saveFileAs() {
        int returnValue = fileChooser.showSaveDialog(null);
        if (returnValue == JFileChooser.APPROVE_OPTION) {
            File selectedFile = fileChooser.getSelectedFile();
            try {
                BufferedWriter writer = new BufferedWriter(new FileWriter(selectedFile));
                textArea.write(writer);
                writer.close();
                isTextSaved = true;
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    private void handleWindowClosing() {
        if (!isTextSaved) {
            int result = JOptionPane.showConfirmDialog(frame, "Do you want to save the changes before closing?",
                    "Unsaved Changes", JOptionPane.YES_NO_CANCEL_OPTION);

            if (result == JOptionPane.YES_OPTION) {
                saveFile();
                if (isTextSaved) {
                    frame.dispose();
                }
            } else if (result == JOptionPane.NO_OPTION) {
                frame.dispose();
            }
        } else {
            frame.dispose();
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(new Runnable() {
            public void run() {
                new Basic_Text_Editor();
            }
        });
    }
}
