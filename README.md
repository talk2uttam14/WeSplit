# WeSplit
A SwiftUI project initial learning
Form
Form {
    Section {
        Text("Hello, world!")
    }

    Section {
        Text("Hello, world!")
        Text("Hello, world!")
    }
}

Navigation
NavigationStack {
    Form {
        Section {
            Text("Hello, world!")
        }
    }
    .navigationTitle("SwiftUI")
}
Binding
struct ContentView: View {
    @State private var name = ""

    var body: some View {
        Form {
            TextField("Enter your name", text: $name)
            Text("Hello, world!")
        }
    }
}
Note:- How that uses name rather than $name? That’s because we don’t want a two-way binding here – we want to read the value, yes, but we don’t want to write it back somehow, because that text view won’t change.
ForEach
Form {
    ForEach(0 ..< 100) {
        Text("Row \($0)")
    }
}
when we’re using ForEach to create many views and SwiftUI asks us what identifier makes each item in our string array unique, our answer is \.self, which means “the strings themselves are unique.” This does of course mean that if you added duplicate strings to the students array you might hit problems, but here it’s just fine
import SwiftUI

struct ContentView: View {
    var names = ["Uttam", "Suman", "Ravi", "Anil", "Rajesh", "Sita", "Gita"]
    @State private var name = ""
    var body: some View {
        Form {
            Section {
                TextField("Enter your name", text: $name)
                Text("Your name is \(name)" )
            }
            Section {
                Picker(selection: $name) {
                    ForEach(names, id: \.self) { name in
                        Text(name)
                    }
                } label: {
                    Text("Selected \(name)")
                }
            }
            Section {
                ForEach(0 ..< 100) {
                    Text("Row \($0)")
                }
            }
            
        }
    }
}

#Preview {
    ContentView()
}
