// Existing imports remain
import java.awt.*;
import java.awt.event.KeyAdapter;
import java.awt.event.KeyEvent;
import java.util.HashMap;
import javax.swing.*;
import javax.swing.border.EmptyBorder;
import javax.swing.border.LineBorder;
import java.util.Map;

public class StylishEmotionBot extends JFrame {
    private JTextArea chatArea;
    private JTextField userInput;
    private Map<String, String> responses;

    public StylishEmotionBot() {
        // Initialize responses map
        initializeResponses();

        // Frame properties
        setTitle("Stylish Emotion Bot");
        setSize(800, 600);
        setDefaultCloseOperation(EXIT_ON_CLOSE);
        setLocationRelativeTo(null);

        // Main panel with gradient background
        JPanel mainPanel = new JPanel() {
            @Override
            protected void paintComponent(Graphics g) {
                super.paintComponent(g);
                Graphics2D g2d = (Graphics2D) g;
                GradientPaint gradient = new GradientPaint(0, 0, new Color(34, 193, 195), getWidth(), getHeight(), new Color(253, 187, 45));
                g2d.setPaint(gradient);
                g2d.fillRect(0, 0, getWidth(), getHeight());
            }
        };
        mainPanel.setLayout(new BorderLayout());

        // Title panel
        JLabel titleLabel = new JLabel("Emotion Detection Chatbot", JLabel.CENTER);
        titleLabel.setFont(new Font("Verdana", Font.BOLD, 28));
        titleLabel.setForeground(Color.WHITE);
        titleLabel.setBorder(new EmptyBorder(10, 10, 10, 10));
        mainPanel.add(titleLabel, BorderLayout.NORTH);

        // Chat area
        chatArea = new JTextArea();
        chatArea.setEditable(false);
        chatArea.setFont(new Font("SansSerif", Font.PLAIN, 16));
        chatArea.setForeground(new Color(50, 50, 50));
        chatArea.setBackground(Color.WHITE);
        chatArea.setBorder(BorderFactory.createCompoundBorder(
                new LineBorder(new Color(173, 216, 230), 2, true),
                new EmptyBorder(10, 10, 10, 10)
        ));
        chatArea.setLineWrap(true);
        chatArea.setWrapStyleWord(true);

        JScrollPane chatScrollPane = new JScrollPane(chatArea);
        chatScrollPane.setBorder(BorderFactory.createEmptyBorder(10, 10, 10, 10));
        mainPanel.add(chatScrollPane, BorderLayout.CENTER);

        // Input panel
        JPanel inputPanel = new JPanel(new BorderLayout());
        inputPanel.setBorder(new EmptyBorder(10, 10, 10, 10));
        inputPanel.setOpaque(false);

        userInput = new JTextField();
        userInput.setFont(new Font("SansSerif", Font.PLAIN, 16));
        userInput.setForeground(Color.DARK_GRAY);
        userInput.setBackground(Color.WHITE);
        userInput.setBorder(new LineBorder(new Color(34, 193, 195), 2, true));
        inputPanel.add(userInput, BorderLayout.CENTER);

        // Add "Enter" key functionality
        userInput.addKeyListener(new KeyAdapter() {
            @Override
            public void keyPressed(KeyEvent e) {
                if (e.getKeyCode() == KeyEvent.VK_ENTER) {
                    handleUserInput();
                }
            }
        });

        mainPanel.add(inputPanel, BorderLayout.SOUTH);

        // Add main panel to frame
        add(mainPanel);
        setVisible(true);

        // Initial bot message
        showWelcomeMessage();
    }


    // Initialize predefined responses
    private void initializeResponses() {
        responses = new HashMap<>();
        responses.put("hello", "Hi there! How can I assist you today?");
        responses.put("hi", "Hello! How are you feeling?");
        responses.put("how are you", "I'm just a bot, but I'm here to listen to you.");
        responses.put("not feeling good", "I'm sorry to hear that. Take a deep breath. Want to talk more about it?");
        responses.put("sad", "I'm here for you. Remember, it's okay to feel sad sometimes. You are not alone.");
        responses.put("happy", "That's great to hear! Happiness is contagious—spread it around!");
        responses.put("tired", "You should rest. Remember, your well-being is important. Can I help with anything?");
        responses.put("angry", "It's okay to feel angry sometimes. Try taking a deep breath or writing down your thoughts.");
        responses.put("stressed", "I'm sorry you're feeling stressed. Try taking a short break or talking to someone you trust.");
        responses.put("excited", "That's amazing! Tell me more about what’s making you excited!");
        responses.put("thank you", "You're welcome! I'm always here for you.");
        responses.put("goodbye", "Goodbye! Take care and have a great day!");
        responses.put("i feel lonely", "I'm sorry to hear that. Remember, you're not alone. What's been on your mind lately?");
        responses.put("i feel lost", "Feeling lost can be tough, but it's part of finding your path. What's been making you feel this way?");
        responses.put("i am anxious", "Anxiety can feel overwhelming. Can you tell me more about what’s causing it?");
        responses.put("i am depressed", "I'm so sorry you're feeling this way. Have you been able to talk to someone about it?");
        responses.put("i feel great", "That's awesome! What’s been making your day so great?");
        responses.put("i feel nervous", "It's okay to feel nervous. What’s coming up that’s making you feel this way?");
        responses.put("i feel overwhelmed", "Take a step back and breathe. What’s the biggest challenge you’re facing right now?");
        responses.put("i feel confused", "That’s okay—confusion is part of learning. What are you trying to figure out?");
        responses.put("i feel excited", "That’s amazing! What are you looking forward to?");
        responses.put("i feel proud", "You deserve to feel proud! What’s the achievement you’re celebrating?");
        responses.put("i feel guilty", "Guilt can be tough to handle. Would you like to talk about it?");
        responses.put("i feel grateful", "Gratitude is such a beautiful emotion. What’s something you’re especially thankful for?");
        responses.put("i feel bored", "Boredom is a sign of creativity waiting to happen. Would you like some suggestions for fun things to do?");
        responses.put("i feel scared", "It’s okay to feel scared. Do you want to share what’s worrying you?");
        responses.put("i feel hopeful", "That’s wonderful! What’s giving you hope right now?");
        responses.put("i feel rejected", "Rejection can hurt, but it doesn’t define your worth. Want to talk about it?");
        responses.put("i feel tired", "Rest is essential. Have you been able to take a break lately?");
        responses.put("i feel frustrated", "It’s okay to feel frustrated. What’s been bothering you?");
        responses.put("i feel relaxed", "That’s great to hear. What’s helping you stay so calm?");
        responses.put("i feel calm", "Staying calm is such a great mindset. How do you manage to stay grounded?");
        responses.put("i am confused about life", "Life can feel overwhelming sometimes. What’s been on your mind?");
        responses.put("i feel empty", "Feeling empty can be hard. What usually helps you feel better?");
        responses.put("i feel loved", "That’s beautiful! Who’s been making you feel this way?");
        responses.put("i feel insecure", "Insecurities are part of being human. What’s been making you feel this way?");
        responses.put("i feel peaceful", "Peace is a wonderful feeling. What’s been helping you stay at ease?");
        responses.put("i feel curious", "Curiosity is the key to discovery! What’s something you’re curious about?");
        responses.put("i feel embarrassed", "Embarrassment happens to everyone—it’s part of being human. What happened?");
        responses.put("i feel nostalgic", "Nostalgia can be bittersweet. What memory is coming to your mind?");
        responses.put("i feel optimistic", "Optimism is such a great mindset. What’s giving you hope?");
        responses.put("i feel pessimistic", "It’s okay to have those feelings. What’s been worrying you?");
        responses.put("i feel annoyed", "Annoyance can be frustrating. What’s been bothering you?");
        responses.put("i feel shy", "It’s okay to feel shy. What situation made you feel this way?");

    }

    // Display the initial welcome message
    private void showWelcomeMessage() {
        chatArea.append("Bot: Hello! I'm your Emotion Bot. How are you feeling today?\n");
    }

    // Handle user input
    private void handleUserInput() {
        String userText = userInput.getText().trim().toLowerCase();
        if (!userText.isEmpty()) {
            userInput.setText("");
            chatArea.append("You: " + userText + "\n");
            String botResponse = generateResponse(userText);
            chatArea.append("Bot: " + botResponse + "\n");
        }
    }

    // Generate empathetic responses based on predefined inputs with more flexibility

    private String generateResponse(String userText) {
        userText = userText.toLowerCase(); // Normalize user input to lowercase

        // Define some emotional responses based on detected emotions
        if (userText.contains("happy") || userText.contains("joy") || userText.contains("excited")) {
            return "That's great! It sounds like you're in a good mood! What made you so happy?";
        }
        else if (userText.contains("sad") || userText.contains("down") || userText.contains("unhappy")) {
            return "I'm sorry to hear that you're feeling sad. Do you want to talk about what's bothering you?";
        }
        else if (userText.contains("angry") || userText.contains("frustrated")) {
            return "I understand that anger can be tough. Would you like to share what's making you feel this way?";
        }
        else if (userText.contains("nervous") || userText.contains("anxious") || userText.contains("worried")) {
            return "It’s okay to feel anxious. What’s on your mind that's making you feel this way?";
        }
        else if (userText.contains("excited") || userText.contains("thrilled")) {
            return "That's awesome! Tell me more about what you're excited about!";
        }
        else if (userText.contains("lonely") || userText.contains("isolated") || userText.contains("alone")) {
            return "I'm sorry you're feeling lonely. I'm here to talk if you need someone to listen.";
        }
        else if (userText.contains("grateful") || userText.contains("thankful")) {
            return "Gratitude is such a positive feeling. What are you grateful for today?";
        }
        else if (userText.contains("depressed") || userText.contains("hopeless")) {
            return "I'm really sorry you're feeling this way. Sometimes it helps to talk to someone. Would you like to share more?";
        }
        else if (userText.contains("stressed") || userText.contains("overwhelmed")) {
            return "It sounds like you're under a lot of pressure. What’s the source of your stress?";
        }
        else if (userText.contains("confused") || userText.contains("lost")) {
            return "It’s okay to feel confused sometimes. What’s on your mind that’s making you feel unsure?";
        }
        // If no emotion is detected, continue the conversation.
        else {
            return "I'm here to listen. Tell me more about how you're feeling.";
        }
    }


    public static void main(String[] args) {
        SwingUtilities.invokeLater(StylishEmotionBot::new);
    }
}
