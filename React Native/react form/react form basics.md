sample component:
```tsx

interface DummyFormModel {
    name: string;
    email: string;
}

function OrderDetailsForm() {
    //form Handling logic
    const [formData, setFormData] = useState<DummyFormModel>({
        name: '',
        email: ''
    });
    const handleInputChange = (field: keyof DummyFormModel, value: string) => {
        setFormData(prevData => ({
          ...prevData,
          [field]: value
        }));
      };
    const handleSubmit = () => {
        console.log('Form Submitted with data:', formData);
    };
  return (
    <View>
      <TextInput
        label="Name"
        value={formData.name}
        onChangeText={(value) => handleInputChange('name', value)}
      />
      <TextInput
        label="Email"
        value={formData.email}
        onChangeText={(value) => handleInputChange('email', value)}
        keyboardType="email-address"
      />
    <Button
        mode="contained"
        onPress={handleSubmit}
      >
        Submit
      </Button>
    </View>
  );
}
```